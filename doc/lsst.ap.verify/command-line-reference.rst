.. py:currentmodule:: lsst.ap.verify

.. program:: ap_verify.py

.. _ap-verify-cmd:

################################
ap_verify command-line reference
################################

This page describes the command-line arguments and environment variables used by :command:`ap_verify.py`.

.. _ap-verify-cmd-basic:

Signature and syntax
====================

The basic call signature of :command:`ap_verify.py` is:

.. prompt:: bash

   ap_verify.py --dataset DATASET --output WORKSPACE

These two arguments are mandatory, all others are optional.

.. _ap-verify-cmd-return:

Status code
===========

:command:`ap_verify.py` returns a status code of ``0`` if the pipeline ran to completion.
If the pipeline fails, the status code will be an interpreter-dependent nonzero value.

.. _ap-verify-cmd-args:

Named arguments
===============

Required arguments are :option:`--dataset` and :option:`--output`.

.. option:: --id <dataId>

   **Butler data ID.**

   Specify data ID to process using :doc:`data ID syntax </modules/lsst.pipe.base/command-line-task-dataid-howto>`.
   For example, ``--id "visit=12345 ccd=1..6 filter=g"``.
   Multiple copies of this argument are allowed.
   If this argument is omitted, then all data IDs in the dataset will be processed.
   
.. option:: --dataset <dataset_name>

   **Input dataset designation.**

   The input dataset is required for all ``ap_verify`` runs except when using :option:`--help`.

   The argument is a unique name for the dataset, which can be associated with a repository in the :ref:`configuration file<ap-verify-configuration-dataset>`.
   See :ref:`ap-verify-dataset-name` for more information on dataset names.

   Allowed names can be queried using the :option:`--help` argument.

.. option:: --dataset-metrics-config <filename>

   **Input dataset-level metrics config.**

   A config file containing a `~lsst.verify.gen2tasks.MetricsControllerConfig`, which specifies which metrics are measured and sets any options.
   If this argument is omitted, :file:`config/default_dataset_metrics.py` will be used.

   Use :option:`--image-metrics-config` to configure image-level metrics instead.

.. option:: -h, --help

   **Print help.**

   The help is equivalent to this documentation page, describing command-line arguments.

.. option:: -j <processes>, --processes <processes>

   **Number of processes to use.**

   When ``processes`` is larger than 1 the pipeline may use the Python `multiprocessing` module to parallelize processing of multiple datasets across multiple processors.
   
.. option:: --image-metrics-config <filename>

   **Input image-level metrics config.**

   A config file containing a `~lsst.verify.gen2tasks.MetricsControllerConfig`, which specifies which metrics are measured and sets any options.
   If this argument is omitted, :file:`config/default_image_metrics.py` will be used.

   Use :option:`--dataset-metrics-config` to configure dataset-level metrics instead.

.. option:: --metrics-file <filename>

   **Output metrics file.**

   The template for a file to contain metrics measured by ``ap_verify``, in a format readable by the :doc:`lsst.verify</modules/lsst.verify/index>` framework.
   The string ``{dataId}`` shall be replaced with the data ID associated with the job, and its use is strongly recommended.
   If omitted, the output will go to files named after ``ap_verify.{dataId}.verify.json`` in the user's working directory.

.. option:: --output <workspace_dir>

   **Output and intermediate product path.**

   The output argument is required for all ``ap_verify`` runs except when using :option:`--help`.

   The workspace will be created if it does not exist, and will contain both input and output repositories required for processing the data.
   The path may be absolute or relative to the current working directory.

.. option:: --silent

   **Do not report measurements to SQuaSH.**

   This flag previously disabled upload of measurements to SQuaSH.
   SQuaSH support has been removed from ap_verify, so this flag has no effect and is deprecated.
