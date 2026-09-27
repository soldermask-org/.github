<p align="center">
  <a href="https://soldermask.shwinnie.com"><img src="https://raw.githubusercontent.com/soldermask-org/.github/main/profile/banner.svg" alt="SOLDERMASK. Place, route, judge." width="100%"></a>
</p>

<h3 align="center">The layout is the half that fails. We make it pass.</h3>

<p align="center">
A lab building the engines that place and route circuit boards,<br>
and the judge that checks every layout before a fab sees it.
</p>

<p align="center">
  <a href="https://soldermask.shwinnie.com"><b>SITE</b></a> &nbsp;·&nbsp;
  <a href="https://solderdocs.shwinnie.com"><b>DOCS</b></a> &nbsp;·&nbsp;
  <a href="https://github.com/soldermask-org/soldermask-bench"><b>BENCH</b></a> &nbsp;·&nbsp;
  <a href="https://soldermask.shwinnie.com/#try-alpha"><b>TRY ALPHA</b></a>
</p>

<img src="https://raw.githubusercontent.com/soldermask-org/.github/main/profile/trail.svg" width="100%" alt="">

```text
  CIRCUIT ━━━▶ PLACE ━━━━━━━▶ ROUTE ━━━━━━━━━▶ JUDGE ━━━━━━━━━▶ FAB
               the placer     Lightcycle       KiCad's DRC      Gerbers, drill, BOM, CPL
```

Writing the circuit got easy. Laying out the board did not. Where the parts go and how the copper joins them is where a board fails, so that is the whole of the work here.

## Programs on the grid

| Program | What it does | Measured |
|---|---|---|
| **Lightcycle** | Our router. It lays every net at once, and a place two nets want costs more each round until one moves. Compiled in Rust. | 230 of 300 bench boards route clean, against 138 for the A\* router on the same placements (27 Sep 2026) |
| **Quorra** | The placer, made to answer to the router. | Best of six placements: 80.4% route clean, against 74.8% for the boards' own designers (694 boards, 5 Sep 2026) |
| **ISOnet** | Predicts whether a placement will route, before routing it. | AUC 0.916 on boards it never saw (14 Sep 2026) |
| **Mendicant** | Reads how hard a board is to route from its connections alone, before a part is placed. | A 287-net photonic mesh, routed with zero crossings |
| **Gea** | A board written as text a model reads and writes back. | 60 of 60 boards read back exactly, in 4.7× to 6.4× fewer tokens than JSON (18 Sep 2026) |
| **Guilty Spark** | Says what the build would about the part under your pointer, before it runs. | In development |

## Repositories

| Repository | What it is |
|---|---|
| [**soldermask-bench**](https://github.com/soldermask-org/soldermask-bench) | A routing benchmark of real circuit boards, judged by KiCad's own design-rule check. The tasks, the referee and every baseline's verdict are open, under MIT. |
| **lightcycle** | The router. Private. |
| **soldermask** | The pipeline, the command line, the workbench and the MCP server. In private alpha: [ask for access](https://soldermask.shwinnie.com/#try-alpha). |

## The bench, public set

186 authors' own boards with their copper stripped. Each router gets 300 seconds a board, and one referee judges them all.

| Router | Routes clean |
|---|---|
| Lightcycle | 140 / 186 (75%) \* |
| A\* (KiCadRoutingTools) | 133 / 186 (72%) |
| freerouting 2.4.1 | 69 / 186 (37%) |

<sub>\* Not a held-out result: Lightcycle's board reader was corrected on 27 Sep 2026 by studying its failures on these same tasks. The bench's README says how, and v1.1 brings a fresh hidden set.</sub>

## How the lab works

- **The router is the judge.** A board passes when every net is closed and the DRC is clean. Nothing else counts.
- **Withdrawn in place.** A number that fails an audit is corrected where it was published.
- **The plainest baseline first.** A model ships only if it beats the simplest thing that could work.
- **Every stage says what it could not do.** Silence costs a fab run to find out.

<img src="https://raw.githubusercontent.com/soldermask-org/.github/main/profile/trail.svg" width="100%" alt="">

<p align="center"><sub><code>END OF LINE</code></sub></p>
