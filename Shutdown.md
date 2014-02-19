Shutdown (global)
--------------

1.  Control-Modul offers a shutdownFormation-Service, positional information (of camera- and position-modul) is still used
    (should be used)
2.  All quadcopters are now at the ground, everything else can shutdown.

Variant a: Control-Modul offers information (to API?) if quadcopters are tracked. In shutdown-routine
    that information can be used to trigger shutdown of rest.

Variant b: Control-Modul offers information (to API?) if shutdown is complete. In shutdown-routine
    that information can be used to trigger shutdown of rest.
