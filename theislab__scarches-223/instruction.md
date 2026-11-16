# Issue

**Title:** Allow pickling from GPU to CPU

## Description

**Use case**
I want to train a reference model on GPU. 
Then I want to map a query onto the reference using only a CPU.
I know the `map_location` parameter exists, but it doesn't fully resolve the issue.

**Issue**
In particular, below is the stacktrace for one error I'm encountering when trying to do the above.

**Solution**
I basically just grabbed a solution posted  and applied it to the `scarches` codebase.


```<locals>._load_scpoli(dir_path)
    557     return scPoli.load(dir_path=dir_path, adata=adata_ref)
    558 else:
--> 559     return scPoli.load(dir_path=dir_path, adata=adata_ref, map_location=torch.device("cpu"))

File /srv/conda/envs/saturn/lib/python3.9/site-packages/scarches/models/base/_base.py:170, in BaseMixin.load(cls, dir_path, adata, map_location)
    167 elif not os.path.exists(adata_path) and load_adata:
    168     raise ValueError("Save path contains no saved anndata and no adata was passed.")
--> 170 attr_dict, model_state_dict, var_names = cls._load_params(dir_path, map_location)
    172 # Overwrite adata with new genes
    173 adata = _validate_var_names(adata, var_names)

File /srv/conda/envs/saturn/lib/python3.9/site-packages/scarches/models/base/_base.py:131, in BaseMixin._load_params(cls, dir_path, map_location)
    128 varnames_path = os.path.join(dir_path, "var_names.csv")
    130 with open(setup_dict_path, "rb") as handle:
--> 131     attr_dict = pickle.load(handle)
    133 model_state_dict = torch.load(model_path, map_location=map_location)
    135 var_names = np.genfromtxt(varnames_path, delimiter=",", dtype=str)

File /srv/conda/envs/saturn/lib/python3.9/site-packages/torch/storage.py:240, in _load_from_bytes(b)
    239 def _load_from_bytes(b):
--> 240     return torch.load(io.BytesIO(b))

File /srv/conda/envs/saturn/lib/python3.9/site-packages/torch/serialization.py:795, in load(f, map_location, pickle_module, weights_only, **pickle_load_args)
    793     except RuntimeError as e:
    794         raise pickle.UnpicklingError(UNSAFE_MESSAGE + str(e)) from None
--> 795 return _legacy_load(opened_file, map_location, pickle_module, **pickle_load_args)

File /srv/conda/envs/saturn/lib/python3.9/site-packages/torch/serialization.py:1012, in _legacy_load(f, map_location, pickle_module, **pickle_load_args)
   1010 unpickler = UnpicklerWrapper(f, **pickle_load_args)
   1011 unpickler.persistent_load = persistent_load
-> 1012 result = unpickler.load()
   1014 deserialized_storage_keys = pickle_module.load(f, **pickle_load_args)
   1016 offset = f.tell() if f_should_read_directly else None

File /srv/conda/envs/saturn/lib/python3.9/site-packages/torch/serialization.py:958, in _legacy_load.<locals>.persistent_load(saved_id)
    954     obj._torch_load_uninitialized = True
    955     # TODO: Once we decide to break serialization FC, we can
    956     # stop wrapping with TypedStorage
    957     deserialized_objects[root_key] = torch.storage.TypedStorage(
--> 958         wrap_storage=restore_location(obj, location),
    959         dtype=dtype)
    961 typed_storage = deserialized_objects[root_key]
    962 if view_metadata is not None:

File /srv/conda/envs/saturn/lib/python3.9/site-packages/torch/serialization.py:215, in default_restore_location(storage, location)
    213 def default_restore_location(storage, location):
    214     for _, _, fn in _package_registry:
--> 215         result = fn(storage, location)
    216         if result is not None:
    217             return result

File /srv/conda/envs/saturn/lib/python3.9/site-packages/torch/serialization.py:182, in _cuda_deserialize(obj, location)
    180 def _cuda_deserialize(obj, location):
    181     if location.startswith('cuda'):
--> 182         device = validate_cuda_device(location)
    183         if getattr(obj, "_torch_load_uninitialized", False):
    184             with torch.cuda.device(device):

File /srv/conda/envs/saturn/lib/python3.9/site-packages/torch/serialization.py:166, in validate_cuda_device(location)
    163 device = torch.cuda._utils._get_device_index(location, True)
    165 if not torch.cuda.is_available():
--> 166     raise RuntimeError('Attempting to deserialize object on a CUDA '
    167                        'device but torch.cuda.is_available() is False. '
    168                        'If you are running on a CPU-only machine, '
    169                        'please use torch.load with map_location=torch.device(\'cpu\') '
    170                        'to map your storages to the CPU.')
    171 device_count = torch.cuda.device_count()
    172 if device >= device_count:

RuntimeError: Attempting to deserialize object on a CUDA device but torch.cuda.is_available() is False. If you are running on a CPU-only machine, please use torch.load with map_location=torch.device('cpu') to map your storages to the CPU.
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fcb7a7f10cb5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.