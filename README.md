<!-- 中文用途说明：开始 -->
# 表格数据清洗与计算｜Polars

> **一句话看懂：清洗和计算大量表格数据。**

| 你想了解什么 | 中文说明 |
|---|---|
| 这个工具能做什么 | 清洗和计算大量表格数据。 |
| 怎么使用 | 通过Python代码整理、筛选、合并和计算表格数据。 |
| 适合谁 | 需要反复处理较大数据表的人。 |
| 主要限制 | 与常用的Pandas写法不同，旧代码需要调整。 |
| 后续可以怎么改 | 检查类型、日期、空值和计算结果是否一致。 |

**当前状态：代码已复制到这个账号；尚未安装或实际运行验证。上面的修改建议还没有实施。**

[查看中文工具总目录](https://github.com/3416461284a-debug/akshare/tree/research-catalog-2026-10-25/%E8%A1%8C%E4%B8%9A%E7%A0%94%E7%A9%B6%E5%B7%A5%E5%85%B7%E7%AE%B1) · [查看各工具的详细评估](https://github.com/3416461284a-debug/akshare/blob/research-catalog-2026-10-25/%E8%A1%8C%E4%B8%9A%E7%A0%94%E7%A9%B6%E5%B7%A5%E5%85%B7%E7%AE%B1/03_%E8%AF%A6%E7%BB%86%E6%8A%A5%E5%91%8A%E5%92%8C%E6%A0%B8%E9%AA%8C%E8%AE%B0%E5%BD%95/%E7%83%AD%E9%97%A8%E5%B7%A5%E5%85%B7%E7%BC%BA%E9%99%B7%E4%B8%8E%E6%94%B9%E9%80%A0%E6%8A%A5%E5%91%8A.md)

中文用途整理日期：2026年10月25日。
<!-- 中文用途说明：结束 -->

---

<details>
<summary>原项目详细说明（点击展开）</summary>

<h1 align="center">
  <a href="https://pola.rs">
    <img src="https://raw.githubusercontent.com/pola-rs/polars-static/master/banner/polars_github_banner.svg" alt="Polars logo">
  </a>
</h1>

<div align="center">
  <a href="https://crates.io/crates/polars">
    <img src="https://img.shields.io/crates/v/polars.svg" alt="crates.io Latest Release"/>
  </a>
  <a href="https://pypi.org/project/polars/">
    <img src="https://img.shields.io/pypi/v/polars.svg" alt="PyPi Latest Release"/>
  </a>
  <a href="https://www.npmjs.com/package/nodejs-polars">
    <img src="https://img.shields.io/npm/v/nodejs-polars.svg" alt="NPM Latest Release"/>
  </a>
  <a href="https://community.r-multiverse.org/polars">
    <img src="https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fcommunity.r-multiverse.org%2Fapi%2Fpackages%2Fpolars&query=%24.Version&label=r-multiverse" alt="R-multiverse Latest Release"/>
  </a>
  <a href="https://doi.org/10.5281/zenodo.7697217">
    <img src="https://zenodo.org/badge/DOI/10.5281/zenodo.7697217.svg" alt="DOI Latest Release"/>
  </a>
</div>

<p align="center">
  <b>Documentation</b>:
  <a href="https://docs.pola.rs/api/python/stable/reference/index.html">Python</a>
  -
  <a href="https://docs.rs/polars/latest/polars/">Rust</a>
  -
  <a href="https://pola-rs.github.io/nodejs-polars/index.html">Node.js</a>
  -
  <a href="https://pola-rs.github.io/r-polars/index.html">R</a>
  |
  <b>Agents</b>:
  <a href="https://github.com/polars-inc/skills/tree/main/polars">Skill</a>
  -
  <a href="https://docs.pola.rs/user-guide/misc/polars_llms/">MCP</a>
  |
  <a href="https://docs.pola.rs/">User guide</a>
  |
  <a href="https://discord.gg/4UfP5cfBE7">Discord</a>
</p>

## Polars: Extremely fast Query Engine for DataFrames

Polars is an analytical query engine for DataFrames, written in Rust. It is designed to be fast,
easy to use and expressive. Key features are:

- **Fast**: written from the ground up in Rust with multi-threaded, vectorized (SIMD) execution
- **Lazy & eager execution**: with query optimization out of the box
- **Larger-than-RAM**: the streaming engine processes datasets that don't fit in memory
- **Expressive API**: compose complex queries with powerful expressions
- **Extensible**: extend Polars natively with custom code through
  [I/O and Expression plugins](https://docs.pola.rs/user-guide/plugins/)
- **Multi-language**: bindings for Python, Rust, Node.js, R, and SQL
- **GPU support**: optionally accelerate queries on NVIDIA GPUs
- **Interoperable**: uses the
  [Apache Arrow Columnar Format](https://arrow.apache.org/docs/format/Columnar.html) for zero-copy
  data sharing

To learn more, read the [user guide](https://docs.pola.rs/).

## Polars in action

Queries are composed from expressions. This lazy query gets optimized out of the box and runs in
parallel across all available cores:

```python
import polars as pl

df = (
    pl.scan_parquet("orders.parquet")
    .filter(pl.col("status") == "shipped")
    .group_by("customer_id")
    .agg(
        pl.col("amount").sum().alias("total"),
        pl.len().alias("n_orders"),
    )
    .sort("total", descending=True)
    .collect()
)
```

## Performance

Polars is very fast. In fact, it is one of the best performing Dataframe solutions available. See
the [PDS-H benchmarks](https://www.pola.rs/benchmarks.html) results.

### Handles larger-than-RAM data

If you have data that does not fit into memory, Polars' query engine is able to process your query
(or parts of your query) in a streaming fashion. This drastically reduces memory requirements, so
you might be able to process your 250GB dataset on your laptop. Collect with
`collect(engine='streaming')` to run the query streaming.

## Installation

### Python

Install the latest Polars version with:

```sh
pip install polars
```

See the [User Guide](https://docs.pola.rs/user-guide/installation/#feature-flags) for more details
on optional dependencies

<details>
<summary><b>Compile Polars from source</b></summary>

If you want a bleeding edge release you should compile Polars from source. Advanced users can also
compile for maximum performance for their architecture.

This can be done by going through the following steps in sequence:

1. Install the latest [Rust compiler](https://www.rust-lang.org/tools/install)
2. Install [maturin](https://maturin.rs/): `pip install maturin`
3. `cd py-polars` and choose one of the following:
   - `make build`, slow binary with debug assertions and limited symbols, fast compile times
   - `make build-debug`, same as `make build`, but with all symbols, produces large binaries
   - `make build-release`, fast binary without debug assertions, minimal debug symbols, long compile
     times
   - `make build-nodebug-release`, same as build-release but without any debug symbols, slightly
     faster to compile
   - `make build-debug-release`, same as build-release but with full debug symbols, slightly slower
     to compile
   - `make build-dist-release`, fastest binary, extreme compile times

By default the binary is compiled with optimizations turned on for a modern CPU. Specify `LTS_CPU=1`
with the command if your CPU is older and does not support e.g. AVX2.

Note that the Rust crate implementing the Python bindings is called `py-polars` to distinguish from
the wrapped Rust crate `polars` itself. However, both the Python package and the Python module are
named `polars`, so you can `pip install polars` and `import polars`.

</details>

Check the [Installation guide](https://docs.pola.rs/user-guide/installation/) for more advanced
installations. For example when you expect more than 2^32 (~4.2 billion) rows, run on an old CPU
(e.g. dating from before 2011), or on an `x86-64` build of Python on Apple Silicon under Rosetta.

## Contributing

Want to contribute? Read our [contributing guide](https://docs.pola.rs/development/contributing/)
and check the issue tracker for accepted issues.

Contributors new to the codebase can look for the `good first issue` label to get familiar with the
project.

You can [join the Polars Discord server](https://discord.gg/4UfP5cfBE7) for any help along the way.

## Distributed Polars

Running into hardware limitations executing your queries? Read how you can
[horizontally scale your Polars query on a cluster](https://docs.pola.rs/polars-cloud/).

## License

Polars is licensed under the [MIT License](LICENSE) (SPDX: `MIT`).


</details>
