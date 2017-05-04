Introduction
============

Input/output (I/O)
------------------

Let’s read our data.

I created the database with the cytominer-database application.

.. code-block:: python

    connection = "sqlite:///data/example.sqlite"

    intensities = pandas.read_sql_table("view_intensities", connection)

I’ve extracted the intensity features from the `view_intensities` table.

I can easily filter my features. Let’s filter by the well identifier:

.. code-block:: python

    identifiers = ["A01", "A02", "A10", "A11"]

    measurements = intensities[intensities["g_well"].isin(identifiers)]

.. code-block:: python

    len(measurements)

Quality control (QC)
--------------------

.. code-block:: python

    debris_removed = measurements[measurements["q_debris"] == 0]

Imputation
----------

.. code-block:: python

    feature_columns = [column for column in measurements.columns if column.startswith("m_")]

    na_rows_removed = measurements.dropna(subset=feature_columns)

Normalization
-------------

Feature selection
-----------------
