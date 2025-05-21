Wind Turbine Generator Predictive Maintenance Model
===================================================

Overview
--------

This documentation presents a predictive maintenance model developed for a wind turbine generator using MATLAB/Simulink. It includes system behavior analysis, observed simulation anomalies, and the engineering solutions applied during development. The scope visuals and diagnostics offer insight into the model's evolution and performance improvements.

Development Progress & Diagnostics
----------------------------------

The following sections describe the key simulation outputs, observed issues, and corrective measures applied:

Simulink Scopes Output
^^^^^^^^^^^^^^^^^^^^^^

.. image:: scopes.jpg
   :alt: Simulation Scopes Overview
   :align: center
   :width: 600px

Rotor Speed Panel
^^^^^^^^^^^^^^^^^

- **Observation:** Rotor speed fluctuated slightly around ~1400 RPM.
- **Interpretation:** Speed control was mostly stable, though minor noise was observed.
- **Fix:** Actuator gain was fine-tuned and the speed signal properly scaled (rad/s to pu).

Electromagnetic Torque (Te)
^^^^^^^^^^^^^^^^^^^^^^^^^^^

- **Observation:** Torque signal showed sudden drops and rises.
- **Issue:** Mismatch between actuator dynamics and generator response.
- **Fix:** Added damping through the `Actuator Dynamics` block for smoother torque transitions.

Degradation Growth
^^^^^^^^^^^^^^^^^^

- **Observation:** Gradual increase in degradation over time.
- **Result:** Validates the degradation model based on torque, vibration, and environmental input.
- **Usage:** These values are used for health estimation and predictive maintenance.

Gearbox Output (Unexpected Behavior)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- **Observation:** Flatline at zero — no expected torque transmission.
- **Issue:** Incorrect signal connection between torque input and gearbox.
- **Fix:** Rerouted torque path and reconnected the gearbox output.

Vibration RMS & Statistical Metrics
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- **Observation:** Sporadic spikes in vibration RMS and kurtosis.
- **Insight:** Likely caused by injected faults or rotor/generator misalignment.
- **Response:** Introduced `generator_vibration_sensor` to extract meaningful fault features.

.. note::

   All signals shown above represent time-based samples with a simulation period of T = 100000.

Potential Improvements
----------------------

- Implement fault injection for gearbox and blade degradation
- Integrate machine learning models for RUL (Remaining Useful Life) estimation
- Enhance cycle factor metrics based on real turbine usage
- Add weather input via `.mat` or `.csv` datasets

License & Credits
-----------------

- Base model © 2009–2020 The MathWorks, Inc.
- Extensions and modifications by Hachim & Abdellah
- **Academic use only**
