# MD80 ROS2 Node

This node handles the communication between MAB's MD80 drives in ROS2 environment. The node was designed to act as 
operational endpoint - to control the drives and get information from them, thus it is not capable of configuring the drives, 
for this use [MDtool](https://github.com/mabrobotics/mdtool).

## Principles of operation

The node normally communicates via services for setup, and via topics for regular data transfers.
Services are: 
```
/add_md80s
/zero_md80s
/set_mode_md80s
/enable_md80s
/disable_md80s
/clear_error_md80s
/get_full_status_md80s
```

Topics subscribed by the node are:
```
/md80/motion_command
/md80/impedance_command
/md80/velocity_pid_command
/md80/position_pid_command
```

Topic published by the node is:
```
/md80/joint_states
/md80/joint_status
```

### Error handling
While an error occures on MD80 while in UPDATE mode (after calling `/enable_md80s`),
the node will produce a message on topic `/md80/joint_status`.

The full status/warning/error state can be read with a call to `/get_full_status_md80s` service,
and cleared with a call to `/clear_error_md80s` service.

NOTE: Both of the above services will disable all drives connected in same CAN  netowrk as md80,
that signaled an error. Clearing errors is not possible without disabling the drives.
This is intended safety feature.


## Quick startup guide

Please find a detailed startup guide in the [MD80 x CANdle manual](https://www.mabrobotics.pl/servos)
