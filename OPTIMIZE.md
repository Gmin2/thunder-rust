# Thunder-Rust Performance Optimization

## What I Changed and Why

I optimized  sync performance by changing. 

-  **Parallelized transaction processing** by adding a `SyncRoTxn` wrapper to make database reads thread-safe, enabling concurrent `fill_transaction` calls using `par_iter()`.

-  **Increased signature verification batch size** from 4096 to 16384 in `verify_authorizations()` to reduce thread synchronization overhead while maintaining cache efficiency

-  **Replaced streaming Blake3 hasher** with single-shot `blake3::hash()` in `get_address()` to eliminate streaming API overhead

-  **Added early exit optimizations** for empty authorization lists to avoid unnecessary computations.

I have obtained a [sync-time](https://github.com/Gmin2/thunder-rust/actions/runs/16241133331/job/45857707456) of 56.77s which is about 5.78% improvement over the previous time of 60.037s