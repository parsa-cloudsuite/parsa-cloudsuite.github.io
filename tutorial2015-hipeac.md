---
layout: page
title: Server Benchmarking with CloudSuite 3.0
---


<p>
<ul>
<li><b>Where?</b> In conjuction with <a href="https://www.hipeac.net/2016/prague/schedule/#tutori">HiPEAC </a> in Prague, Czech Republic.</li>
<li><b>When?</b> January 20th, 2016.</li>
<li><b>Intended audience:</b> Academic/industrial researchers interested in scale-out datacenter workloads and their performance evaluation via both existing state- of-the-art servers and cycle-accurate simulation.</li>
<li><b>Team:</b> Alexander Daglis, Mario Paulo Drumond, Tapti Palit, Javier Picorel, Babak Falsafi, Mike Ferdman of EPFL and Stonybrook.</li>
<li><b>Keywords:</b> Scale-out workloads, server benchmarking, rigorous measurement methodologies, performance evaluation.</li>
<li><b>Registration:</b> Please follow the registration link on the <a href="https://www.hipeac.net/2016/prague/">conference web page</a>.</li>
</ul>
</p>

<br/>
<h1>Tutorial In Brief</h1>
<p>
Since its inception, CloudSuite (cloudsuite.ch) has emerged as a popular suite of benchmarks both in industry and among academics for scale-out server and services performance evaluation. The EuroCloud Server project blueprinted key optimizations in server SoCs based on the salient features of CloudSuite workloads that lead to an order of magnitude improvement in efficiency while preserving QoS. ARM-based server products (e.g., Cavium ThunderX) have now emerged following these guidelines and showcasing the improved efficiency.
CloudSuite 3.0 is a major enhancement over prior releases both in workloads and infrastructure. It includes benchmarks that represent massive data maniuplation with tight latency constraints such as in-memory data analytics using Apache Spark, a new real-time video streaming benchmark following today’s most popular video-sharing website setups, and a new web serving benchmark mirroring today’s multi-tier web server software stacks with a caching layer.
To ease the deployment of CloudSuite into private and public cloud systems, the benchmarks are integrated into the Docker container system and Google’s PerfKit Benchmarker. PerfKit helps at automate the process of benchmarking with a performance comparison across existing cloud server systems. CloudSuite 3.0 will be released and supported to run both on real hardware and a QEMU- based emulation platform.
</p>

<p>The emergence of cloud computing as a dominant computing platform highlights the need for practical and rigorous architectural evaluation of server systems. Such evaluation mandates the use of a variety of real-world server workloads, all of which are radically different from traditional desktop and scientific benchmarks. Unfortunately, deep and complex software stacks of both conventional (e.g., OLTP, DSS) and emerging scale-out (e.g., Media Streaming, Web Search) server workloads make the evaluation process even harder and slower, postponing the adoption of realistic server benchmarks within the architectural community.<p>
<p><a href="{{ site.baseurl }}">CloudSuite</a> is an on-going effort towards a common architectural evaluation basis, aimed at providing an up-to-date suite of benchmarks that represent popular scale-out cloud applications commonly found in today’s datacenters. The latest version, CloudSuite 2.0, comprises of eight scale-out applications that feature real-world server software stacks and datasets that can be used as realistic benchmarks for the scale-out applications class. These applications are data analytics, data caching, data serving, graph processing, media streaming, software testing, web search, and web serving. CloudSuite provides the means for throughput and quality of service (QoS) measurement for each benchmark.</p> 
<p>In this tutorial, we first introduce CloudSuite 2.0 and demonstrate how to run the benchmarks on real hardware. As evaluating server software stacks via full-system simulation is prohibitively slow, a need for statistical sampling emerges. A rigorous sampling methodology is of utmost importance, because improper sampling can lead to highly misleading results. Devising the right sampling methodology for server workloads is not trivial. For that reason, our tutorial covers the SMARTS sampling methodology, a widely applicable framework that enables fast cycle-accurate simulation of both conventional and emerging server workloads on various full-system architectural simulators. We demonstrate how the SMARTS methodology can be applied in today’s simulators through a case study; we describe the complete simulation process using <a href="http://parsa.epfl.ch/simflex/">Flexus</a>, a full-system multiprocessor simulator that leverages the statistical sampling methodology for fast, yet rigorous evaluation of CloudSuite 2.0 benchmarks.</p>

<br/>


<h1>Detailed Program</h1>

<p>The emergence of cloud computing as a dominant computing platform highlights the need for architectural evaluation of cloud server systems. Moreover, the fast emergence of new applications and techniques to manipulate the massive amounts of data generated by the popular cloud applications mandates a continuous update to existing benchmarks and architectural evaluation infrastructure. In this tutorial, we will present CloudSuite 2.0, the latest release of <a href="http://parsa.epfl.ch/cloudsuite/cloudsuite.html">CloudSuite</a> that includes popular open-source benchmarks. We will highlight the key differences between cloud applications and traditional benchmarks used for architectural evaluation. Because evaluating the full software stack of modern cloud applications using existing cycle-accurate software simulators is prohibitively slow, sampling the execution is essential. We will introduce the <a href = "SMARTS.pdf">SMARTS</a> statistical sampling methodology, which enables fast and rigorous simulation of complex systems running real-world server software, such as CloudSuite. We will further demonstrate how the SMARTS methodology can be seamlessly integrated into today's simulators, using the <a href="http://parsa.epfl.ch/simflex/">Flexus</a> simulation infrastructure as an example.  </p>
<p>CloudSuite is an on-going effort that aims to provide an up-to-date suite of benchmarks that represent popular scale-out applications. CloudSuite 2.0 is the second release of CloudSuite and includes new benchmarks that represent existing trends in manipulating massive data, such as data caching and graph analytics. CloudSuite 2.0 is based on real-world full-system software stacks and datasets and takes into account quality of service (QoS) performance metrics. </p>
<p>We provide support for running CloudSuite 2.0 both on real hardware and within architectural simulators, such as Flexus. Simics images that are compatible with the Flexus infrastructure are available for download. The Flexus component-based design allows for the composition of complex multicore systems, enabling rapid evaluation of the architectural behavior of cloud applications on a wide range of processor organizations and microarchitectures. Flexus achieves fast simulation turnaround while ensuring representative results by leveraging the SMARTS simulation sampling methodology, which will be thoroughly covered in this tutorial.</p>
<p>Our tutorial is organized as follows. First, we present an overview of CloudSuite 2.0, providing details on the software stacks constituting each benchmark, and steps to run the benchmarks on real hardware. The second session of our tutorial makes the case for careful sampling-based simulation of CloudSuite applications, which is essential for making detailed simulation of reasonable execution windows feasible. We present the relevant sampling background and explain how the SMARTS methodology can be applied to enable fast and accurate evaluation of systems running CloudSuite regardless of the underlying simulation infrastructure. We proceed with an overview of Flexus as a case study of a cycle-accurate full-system simulator that applies statistical sampling to allow for fast simulation of complex multicore systems running real server benchmarks. We demonstrate Flexus' anatomy, how to use the preconfigured multicore organizations and microarchitectures, and how to add and simulate new components.</p>

<h4>(Tentative) Agenda</h4>
<table cellspacing="8" border="0">
<tr id="row1"  >
<td width="20%" align="center">Time Slot</td><td>Topic</td><td>Material</td>
</tr>
<tr align="center"><td>1:30pm - 2:15pm</td><td>CloudSuite 2.0</td><td>Overview of CloudSuite 2.0 benchmarks and running them on real hardware</td>
</tr>
<tr align="center"><td>2:15pm - 2:45pm</td>
<td>CloudSuite Full-System Simulation </td>
<td>Introduction to Flexus and its interaction with the Simics full-system simulator </tr>
<tr align="center"><td>2:45pm - 3:15pm</td><td><em>Coffee Break</em></td><td></td><td></td></tr>
<tr align="center"><td>3:15pm - 3:45pm</td><td>Fast and Detailed Simulation Using Flexus</td><td>Demonstrating Flexus internals and how to perform detailed microarchitectural simulation </td>
</tr>
<tr align="center"><td>3:45pm - 4:30pm</td><td>Statistical Sampling</td><td>Making detailed simulation fast using SMARTS sampling methodology</td>
<tr align="center"><td>4:30pm</td><td> Wrap-up </td></tr>
</tr>
</table>

<br/>
<h4>Organizer</h4>


<ul>
<a href="http://parsa.epfl.ch/~kocberbe">Onur Kocberber</a> is a fifth-year PhD candidate in the Parallel Systems Architecture Laboratory at EPFL, advised by Prof. Babak Falsafi. Onur's research focuses on design for dark silicon and efficient server architectures for large-scale datacenters.
<!--
<li> <a href="http://parsa.epfl.ch/~jevdjic">Djordje Jevdjic</a> is a fifth-year PhD candidate in the Parallel Systems Architecture Laboratory at EPFL, advised by Prof. Babak Falsafi. Djordje works on high-performance memory systems for servers, including on-chip DRAM caches and 3D-die stacking, with emphasis on locality and energy-efficiency.</li>
<li> <a href="http://parsa.epfl.ch/~kaynak">Cansu Kaynak</a> is a fifth-year PhD candidate in the Parallel Systems Architecture Laboratory at EPFL, advised by Prof. Babak Falsafi. Cansu's research focuses on high-performance memory systems to bridge the ever-increasing processor/memory performance gap. She is currently working on mitigating instruction-related stalls, a key performance bottleneck in server applications.</li> 
<li> <a href="http://parsa.epfl.ch/~volos">Stavros Volos</a> is a fifth-year PhD candidate in the Parallel Systems Architecture Laboratory at EPFL, advised by Prof. Babak Falsafi. Stavros's work focuses on energy-efficient memory systems for server applications, with emphasis on energy-efficient data movement.</li><
-->

</ul>