<!-- Tab Navigation -->
<div class="tabs">
  <button class="tablinks" onclick="openTab(event, 'overview')" id="defaultOpen">Overview</button>
  <button class="tablinks" onclick="openTab(event, 'report')">Project Report (PDF)</button>
</div>

<!-- Tab Contents -->

<div id="overview" class="tabcontent" markdown="block">
<!-- Put your Overview Markdown content here -->
<h2>Project Overview</h2>

# Parallel Union Find

---
<!-- 
## Team Members
Zhaowei Zhang, Eric Zhu -->

## Project Website

[https://github.com/pentene/15418-final-project](https://github.com/pentene/15418-final-project)

---

## Summary

In this project, we will explore different lock techniques of the Union-find data structure, specifically coarse-grained lock, fine-grained lock, and lock-free along with Union-Find
specific optimizations (path compression, union by rank). We aim to benchmark these implementations rigorously, analyzing their performance characteristics and scalability compared
to the serialized version. Finally, we plan to test our implementation in different graph algorithms to further analyze its performance in real-world applications.

---

## Background

The Union-Find data structure is essential in applications that require efficient detection of connectivity, such as clustering, graph connectivity, and image segmentation. The two
fundamental operations are find and union. Parallelizing these operations requires careful handling of concurrent access to shared memory structures, along with optimizations such as
path compression and union by rank. Parallelism combined with these optimizations significantly enhances performance for
large-scale sets. Efficient synchronization must be paired with effective optimizations to achieve peak performance

---

## Goals and Deliverables

Planned Goals:

- Implement Multiple parallel implementations on CPU with OpenMP using coarse-grained lock, fine-grained lock, and lock-free techniques.

- Implementation of Union-Find optimizations (path compression, union by rank) along with synchronization methods

- Measure and compare throughput, latency, and scalability of each synchronization and optimization method on CPU under diverse workloads, including: varying graph sizes and densities (sparse, dense),
different access patterns (find-heavy, union-heavy workloads), and real-world datasets.

Aspirational Goals:

- Investigate dynamic selection of locking vs. lock-free approaches depending on workload size or distribution.

- Demonstrate parallel Union-Find performance improvements in practical applications such as image segmentation or network analysis.

Fallback Goals:

- Focus on fewer synchronization methods and optimizations with a thorough performance analysis.

- Identify the potential bottlenecks in the parallel algorithms. 

---

## Challenges

Parallelizing and optimizing Union-Find using OpenMP on CPUs presents several signif-
icant challenges, driven primarily by workload characteristics, synchronization complexity,
and architectural constraints:

- Workload Characteristics: While many find and union operations can run concurrently, conflicts can arise when multiple threads simultaneously update shared structures (parent and rank arrays). Proper synchronization methods must mitigate these conflicts without severely limiting concurrency. And this is one important field we will be testing on.

- Memory access characteristics: Union-Find operations, especially with path compression, lead to irregular memory access patterns. These irregular accesses result in scattered memory reads and writes, limiting cache performance and reducing locality.

- Communication-to-Computation ratio: Despite the simplicity of union-find computations, synchronization overhead can dominate performance, particularly with frequent concurrent updates.

- Divergent execution: The pointer-chasing nature of Union-Find, particularly path compression, inherently generates unpredictable branching and memory access, complicating optimization and efficient parallel execution on CPUs.

By addressing these challenges specifically within the context of OpenMP, we aim to
deepen our understanding of parallel programming principles, synchronization mechanisms,
and efficient optimization strategies tailored for shared-memory multicore systems.

---

## Resources

Implementation and benchmarking will be performed primarily on GHC lab machines and Pittsburgh Supercomputing Center (PSC) resources. Initial sequential implementations will be verified against OpenCV’s bilateral filter for correctness. 
PSC machines offer robust CPU and GPU capabilities for detailed performance profiling and large-scale experimentation.

Here is our current reference:

- Tomasi, C., & Manduchi, R. (1998). Bilateral filtering for gray and color images. Proceedings of the Sixth International Conference on Computer Vision, 839–846.

- Paris, S., & Durand, F. (2006). A fast approximation of the bilateral filter using a signal processing approach. European Conference on Computer Vision, 568–580.

- Paris, S., Kornprobst, P., Tumblin, J., & Durand, F. (2009). Bilateral filtering: Theory and applications. Foundations and Trends in Computer Graphics and Vision, 4(1), 1–73.

- [Nvidia documentation on bilateral filtering](https://docs.nvidia.com/vpi/algo_bilat_filter.html)

---

## Platform Choice

The GHC lab machines and PSC machines provide multi-core CPUs and GPU resources
suitable for our parallel implementations. GHC machines will facilitate development and
initial testing, while the powerful GPU systems at PSC will enable detailed performance
profiling and large-scale experimentation.

---

## Schedule (Tentative)

|   Week   | Planned Acrivity |
| -------- | ------- |
| 3.26 - 4.2  | Implement serial version of bilateral filter; begin OpenMP parallelization |
| 4.2 - 4.9   | Analyze CPU performance, identify bottlenecks, and optimize OpenMP parallelization using course techniques |
| 4.9 - 4.16  | Develop initial CUDA implementation; perform GPU profiling and identify bottlenecks |
| 4.16 - 4.23 | Optimize CUDA implementation based on analysis; evaluate GPU performance improvements |
| 4.23 - 4.28 | Finalize benchmarking results, prepare poster and presentation materials |
| 4.29        | Poster session |

</div>

<div id="report" class="tabcontent">
  <h2>Project Report</h2>
  <iframe src="assets/15418_Project_Proposal.pdf" width="100%" height="800px"></iframe>
</div>

<script>
function openTab(evt, tabName) {
  var i, tabcontent, tablinks;

  tabcontent = document.getElementsByClassName("tabcontent");
  for (i = 0; i < tabcontent.length; i++) {
    tabcontent[i].style.display = "none";
  }

  tablinks = document.getElementsByClassName("tablinks");
  for (i = 0; i < tablinks.length; i++) {
    tablinks[i].className = tablinks[i].className.replace(" active", "");
  }

  document.getElementById(tabName).style.display = "block";
  evt.currentTarget.className += " active";
}

// Open the default tab on load
document.getElementById("defaultOpen").click();
</script>

<style>
.page-content {
max-width: 2400px; /* Adjust to your desired width */
margin: 0 auto;    /* Centers the content horizontally */
padding: 0 20px;   /* Adds a bit of padding on sides */
}

.tabs {
  overflow: hidden;
  border-bottom: 1px solid #ccc;
}

.tablinks {
  background-color: inherit;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 10px 15px;
  transition: 0.3s;
  font-size: 16px;
}

.tablinks:hover {
  background-color: #ddd;
}

.tablinks.active {
  background-color: #ccc;
}

.tabcontent {
  display: none;
  padding: 15px;
  border-top: none;
}
</style>


