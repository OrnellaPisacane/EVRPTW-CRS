# README — Results File Structure

## Directory layout

Top‑level directories represent **runtime budgets** for the experiments. The repository includes folders named **“10 minutes”** and **“60 minutes”**, which contain results obtained with a 10‑minute and a 60‑minute time limit, respectively.

Inside each runtime directory:

* There is **one subdirectory per algorithm configuration**. These directories are named following the pattern:

  * `alns_{i}p_{recharge}_{time}`

    * `{i}`: capacity of the charging stations.
    * `{recharge}`: recharge type (`pwl`, `linear`).
    * `{time}`: computation time setting for that algorithm run.
* Within each subdirectory, there are **`.ris`** files corresponding to individual runs.

**Filename convention (per run):**

* `<instance>_<customers>_<seed>.ris`

  * `<instance>`: instance identifier (e.g., `c101`).
  * `<customers>`: number of customers.
  * `<seed>`: run seed.

---

## `.ris` file schema

Each `.ris` file is a JSON object with the following keys:

* **`construction_solution`**: Initial solution produced by first construction.

  * `cost`: Objective value (very large if infeasible).
  * `feasible`: Whether the solution meets all constraints.
  * `journeys`: List of routes, each route is a list of node IDs.
  * `n_vehicles`: Number of vehicles/routes.

* **`incumbents`**: Chronological list of best‑so‑far solutions found during the run.

  * Each entry has `cost` and `time` (seconds since start).

* **`iterations`**: Number of iterations executed in the run.

* **`solution`**: Final best solution.

  * Same structure as `construction_solution`.

* **`time`**: total wall‑clock time.

---

## Node identifiers

* **`D0`**: Depot.
* **`C<i>`**: Customer.
* \`S\<i>-\<j>\`: Service station \<i>, pump \<j>.
