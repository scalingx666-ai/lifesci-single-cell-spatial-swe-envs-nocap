# Issue

**Title:** Refactor/remove protocol classes

## Description

Solves 

There are some **cons** atm:

- I used Any  annotations in the abstract classes which is less specific than most of the protocols. See for example:
```python

class AbstractSolutionsProblems(ABC, metaclass=CombinedMeta):

    @property
    @abstractmethod
    def solutions(self) -> Any:
        """Solutions."""
        pass

    @property
    @abstractmethod
    def problems(self) -> Any:
        """Problems."""
        pass

    @property
    @abstractmethod
    def _policy(self) -> Any:
        """Subset policy."""
        pass
```
- For example one class uses src vs tgt terminology ( and other uses sp vs sc. They are essentially the same but I just rewrote them as is as two abstract classes. Otherwise it might also require more time to unify them.
These are the two classes I am talking about:
```python
class AbstractSrcTgt(ABC, metaclass=CombinedMeta):

    @property
    @abstractmethod
    def adata_src(self) -> AnnData:
        """Annotated data object."""
        pass

    @property
    @abstractmethod
    def adata_tgt(self) -> AnnData:
        """Annotated data object."""
        pass


class AbstractSpSc(ABC, metaclass=CombinedMeta):

    @property
    @abstractmethod
    def adata_sp(self) -> AnnData:
        """Annotated data object."""
        pass

    @property
    @abstractmethod
    def adata_sc(self) -> AnnData:
        """Annotated data object."""
        pass
```
- With the GENOT implementation `GENOTLinProblem` tries to inherit a class that requires `push/pull`
https://github.com/theislab/moscot/blob/f84f8be91e09a174edfbd1d4985e2dd575c0eafc/src/moscot/problems/generic/_generic.py#L779
**pros:**

- Less ignore comments for mypy
- Less code
- Better understanding of the expected attributes and methods


Things to do:
- Decide which files these new abstract classes should be in final version.
- Maybe fix the cons if important

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ed48242a270e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.