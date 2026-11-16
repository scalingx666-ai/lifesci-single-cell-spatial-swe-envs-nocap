# Issue

**Title:** Added general-purpose handler for long-term download caching.

## Description

```html
<html>
<script type="module">
import * as thing from "./DownloadsDBHandler.js";
await thing.initialize();
await thing.remove("https://anime-gifs.aaron-lun.workers.dev/random/gif");
let stuff = await thing.get("https://anime-gifs.aaron-lun.workers.dev/random/gif");
console.log(stuff);
let stuff2 = await thing.get("https://anime-gifs.aaron-lun.workers.dev/random/gif");
console.log(stuff2); # same size, retrieved from cache.
</script>
</html>
```

The immediate pickle is that the SinglePP references are held as GitHub Artifacts, and those don't have CORS enabled. We'll have to move them to a GH pages location to be able to download them properly.

A more general concern is the fact that IndexedDB has this strange auto-committing behavior whereby the transaction closes on the last callback. This seems to imply that we cannot do any asynchronous operations after the first request, which means that I can't, e.g., read the database, download the file and save it in a single transaction. Right now I'm using two transactions, which has implications for multiple queries - for example, if you remove the `await`s above, you'll get two different buffer sizes. 

(The second point also makes me think about some of our single-transaction-multi-request code in `KanaDBHandler.js`. I think it is correct, but its correctness is not obvious, and relies on the timings of operations from a single-threaded process.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a71eef14d0af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.