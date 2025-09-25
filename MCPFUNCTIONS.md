# MCP Functions

This is a list of functions that can be used in the Brewie ROS MCP Server.

## get_topics 
- **Purpose**: Retrieves the list of available topics from the robot's ROS system.
- **Returns**: List of topics (List[Any])

## pub_twist
*Not relevant for Brewie, deleted*
- **Purpose**: Sends movement commands to the robot by setting linear and angular velocities.
- **Parameters**:
  - `linear`: Linear velocity (List[Any])
  - `angular`: Angular velocity (List[Any])

## pub_twist_seq
*Not relevant for Brewie, deleted*
- **Purpose**: Sends a sequence of movement commands to the robot, allowing for multi-step motion control.
- **Parameters**:
  - `linear`: List of linear velocities (List[Any])
  - `angular`: List of angular velocities (List[Any])
  - `duration`: List of durations for each step (List[Any])
 
## sub_image -> get_image
*Changed to auto-open file in Windows*
- **Purpose**: Receive images from the robot's point of view or of the surrounding environment.
- **Parameters**: None
- **Returns**: Image saved to `photos/environment/` directory with timestamp

## pub_jointstate
*Not relevant for Brewie, deleted*
- **Purpose**: Publishes a custom JointState message to the `/joint_states` topic.
- **Parameters**:
  - `name`: List of joint names (list[str])
  - `position`: List of joint positions (list[float])
  - `velocity`: List of joint velocities (list[float])
  - `effort`: List of joint efforts (list[float])

## sub_jointstate
*Not relevant for Brewie, deleted*
- **Purpose**: Subscribes to the `/joint_states` topic and returns the latest JointState message as a formatted JSON string.
- **Returns**: JointState message (str)

## make_step
*New function for Brewie*
- **Purpose**: Move Brewie using its kinematic module.
- **Parameters**:
  - `x`: float(-1.0 to 1.0) - Left/Right movement (1.0 = left, -1.0 = right)
  - `z`: float(-1.0 to 1.0) - Forward/Backward movement (1.0 = forward, -1.0 = backward)
- **Returns**: "one step!" confirmation message

## defend
*New function for Brewie*
- **Purpose**: Defend against opponents by aiming and shooting.
- **Parameters**:
  - `rotate`: float(-1.2 to 1.2) - Horizontal aim position
  - `UPDOWN`: float(-0.3 to 0.2) - Vertical aim position
- **Returns**: "one less threat!" confirmation message

## sniper
*New function for Brewie*
- **Purpose**: Autonomous target detection and shooting using AI vision.
- **Parameters**:
  - `targediscr`: str - Description of the target to shoot
- **Returns**: None (executes shooting sequence)

## BrewPay
*New function for Brewie*
- **Purpose**: Perform SOL cryptocurrency transfer using QR code detection.
- **Parameters**:
  - `amount`: float - Amount in SOL to transfer
- **Returns**: Transfer status message

## run_action
*New function for Brewie*
- **Purpose**: Launch pre-prepared actions in the Brewie application.
- **Parameters**:
  - `action_name`: str - Name of the action to execute (without .d6a extension)
- **Returns**: Action execution result

## get_available_actions
*New function for Brewie*
- **Purpose**: Retrieves the list of available pre-prepared actions from ActionGroups.
- **Parameters**: None
- **Returns**: List of available action names (List[str])
