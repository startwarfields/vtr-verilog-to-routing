.. _benchmarks:

Benchmarks
==========

There are several sets of benchmark designs which can be used with VTR.

VTR Benchmarks
--------------
The VTR benchmarks :cite:`luu_vtr,luu_vtr_7` are a set of medium-sized benchmarks included with VTR.
They are fully compatible with the full VTR flow.
They are suitable for FPGA architecture research and medium-scale CAD research.



.. _table_vtr_benchmarks:

.. table:: The VTR 7.0 Benchmarks.

    ================    =================
    Benchmark           Domain
    ================    =================
    bgm                 Finance
    blob_merge          Image Processing
    boundtop            Ray Tracing
    ch_intrinsics       Memory Init
    diffeq1             Math
    diffeq2             Math
    LU8PEEng            Math
    LU32PEEng           Math
    mcml                Medical Physics
    mkDelayWorker32B    Packet Processing
    mkPktMerge          Packet Processing
    mkSMAdapter4B       Packet Processing
    or1200              Soft Processor
    raygentop           Ray Tracing
    sha                 Cryptography
    stereovision0       Computer Vision
    stereovision1       Computer Vision
    stereovision2       Computer Vision
    stereovision3       Computer Vision    
    ================    =================

The VTR benchmarks are provided as Verilog under: ::

    $VTR_ROOT/vtr_flow/benchmarks/verilog

This provides full flexibility to modify and change how the designs are implemented (including the creation of new netlist primitives).

The VTR benchmarks are also included as pre-synthesized BLIF files under: ::

    $VTR_ROOT/vtr_flow/benchmarks/vtr_benchmarks_blif

.. _titan_benchmarks:

Titan Benchmarks
----------------
The Titan benchmarks :cite:`murray_titan,murray_timing_driven_titan` are a set of large modern FPGA benchmarks.
The pre-synthesized versions of these benchmarks are compatible with recent versions of VPR.

The Titan benchmarks are suitable for large-scale FPGA CAD research, and FPGA architecture research which does not require synthesizing new netlist primitives.

.. note:: The Titan benchmarks are not included with the VTR release (due to their size). However they can be downloaded and extracted by running ``make get_titan_benchmarks`` from the root of the VTR tree.  They can also be `downloaded manually <http://www.eecg.utoronto.ca/~kmurray/titan/>`_.

.. seealso:: :ref:`titan_benchmarks_tutorial`

Koios Benchmarks
-----------------
The Koios benchmarks :cite:`koios_benchmarks` are a set of Deep Learning (DL) benchmarks. 
They are suitable for DL related architecture and CAD research.
There are 19 designs that include several medium-sized benchmarks and some large benchmarks.
The designs target different network types (CNNs, RNNs, MLPs, RL) and layer types (fully-connected, convolution, activation, softmax, reduction, eltwise).
Some of the designs are generated from HLS tools as well.
These designs use many precisions including binary, different fixed point types int8/16/32, brain floating point (bfloat16), and IEEE half-precision floating point (fp16).

..  table_koios_benchmarks:

.. table:: The Koios Benchmarks.  
  
    =================   ======================================
    Benchmark           Description
    =================   ======================================
    clstm_like          CLSTM-like accelerator
    dla_like            Intel-DLA-like accelerator
    lstm                LSTM engine
    tpu_like            Google-TPU-v1-like accelerator
    bnn                 4-layer binary neural network
    tiny_darknet_like   Accelerator for Tiny Darknet    
    gemm_layer          20x20 matrix multiplication engine
    attention_layer     Transformer self-attention layer
    conv_layer          GEMM based convolution
    spmv                Sparse matrix vector multiplication
    robot_rl            Robot+maze application     
    reduction_layer     Add/max/min reduction tree
    softmax             Softmax classification layer
    conv_layer_hls      Sliding window convolution
    eltwise_layer       Matrix elementwise add/sub/mult  
    =================   ======================================

Koios benchmarks are fully compatible with the full VTR flow. Some Koios benchmarks use advanced DSP features that are available in only a few FPGA architectures provided with VTR. This is because they instantiate DSP macros to implement native FP16 multiplications or use the hard dedicated chains, and these are architecture-specific. If users want to use a different FPGA architecture file, they can replace the macro instantiations in the benchmarks with their equivalents from the FPGA architectures they wish to use.

Alternatively, users can disable these advanced features. The macro ``complex_dsp`` can be used for this purpose. If complex_dsp is defined in a benchmark file (using ```define complex_dsp`` in the beginning of the benchmark file), then advanced DSP features mentioned above will be used. If a user wants to run a Koios benchmark with FPGA architectures that don't have these advanced DSP features (for example, the flagship architectures: ``$VTR_ROOT/vtr_flow/arch/timing/k6_frac_N10_*_mem32K_40nm*``), then they can remove the line defining the complex_dsp macro. This enables the same functionality with behavioral Verilog that is mapped to the FPGA soft logic when an architecture without the required macro definitions is used.

The VTR benchmarks are provided as Verilog (enabling full flexibility to modify and change how the designs are implemented) under: ::

    $VTR_ROOT/vtr_flow/benchmarks/verilog/koios

The FPGA architectures with advanced DSP that work out-of-the-box with Koios benchmarks are available here: ::

    $VTR_ROOT/vtr_flow/arch/COFFE_22nm/k6FracN10LB_mem20K_complexDSP_customSB_22nm.*

MCNC20 Benchmarks
-----------------
The MCNC benchmarks :cite:`mcnc_benchmarks` are a set of small and old (circa 1991) benchmarks.
They consist primarily of logic (i.e. LUTs) with few registers and no hard blocks.

.. warning::
    The MCNC20 benchmarks are not recommended for modern FPGA CAD and architecture research.
    Their small size and design style (e.g. few registers, no hard blocks) make them unrepresentative of modern FPGA usage.
    This can lead to misleading CAD and/or architecture conclusions.

The MCNC20 benchmarks included with VTR are available as ``.blif`` files under::

    $VTR_ROOT/vtr_flow/benchmarks/blif/

The versions used in the VPR 4.3 release, which were mapped to :math:`K`-input look-up tables using FlowMap :cite:`cong_flowmap`, are available under::

    $VTR_ROOT/vtr_flow/benchmarks/blif/<#>

where :math:`K=` ``<#>``.

.. _table_mcnc20_benchmarks:

.. table:: The MCNC20 benchmarks.

    =========   ========================================
    Benchmark   Approximate Number of Netlist Primitives
    =========   ========================================
    alu4         934
    apex2       1116
    apex4        916
    bigkey      1561
    clma        3754
    des         1199
    diffeq      1410
    dsip        1559
    elliptic    3535
    ex1010      2669
    ex5p         824
    frisc       3291
    misex3       842
    pdc         2879
    s298         732
    s38417      4888
    s38584.1    4726
    seq         1041
    spla        2278
    tseng       1583
    =========   ========================================

