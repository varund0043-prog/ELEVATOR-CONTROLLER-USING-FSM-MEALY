**Project Overview**
Implements a finite state machine (FSM) elevator controller using Mealy architecture

Manages elevator operations between 4 floors (0 to 3)

Includes door control and overweight detection functionality

** Design Specifications**
Inputs:
clk: System clock

rst: Active-high reset signal

req[3:0]: Floor request buttons (bit 0: floor 0, bit 1: floor 1, etc.)

overweight: Signal indicating elevator is overloaded (prevents door closing)

Outputs:
current_floor[1:0]: Current elevator position (0-3)

door_open: Door status (1 = open, 0 = closed)

moving: Elevator movement status (1 = moving, 0 = stationary)

States:
IDLE: Elevator stationary with doors open

CLOSE_DOOR: Closing doors before movement

MOVE: Moving between floors

** Design Features**
Priority encoder for floor requests (higher floors have priority)

Overweight safety feature prevents door closing when activated

Sequential floor movement (one floor per clock cycle when moving)

Automatic door opening upon reaching destination

** Vivado Implementation Flow**
1. Project Creation
Created new Vivado project (2020.1 or later)

Selected appropriate FPGA device (e.g., xc7a100tcsg324-1)

Added design files: elevator_controller.v and tb_elevator_controller.v

2. Design Synthesis
Run synthesis to convert RTL to gate-level representation

Checked for warnings and critical warnings

Verified resource utilization:

LUTs: ~15-20

Flip-flops: ~10-15

I/O pins: 11

3. Simulation
Configured simulation settings for behavioral simulation

Ran simulation with provided testbench

Verified functionality through waveform analysis:

Reset sequence

Overweight condition handling

Floor request processing

Movement between floors

Door operation

4. Constraints
Created constraints file (elevator_constraints.xdc)

Clock frequency definition (e.g., 100MHz)

I/O pin assignments (if targeting physical hardware)

Timing constraints

5. Implementation
Run implementation to perform:

Placement of design elements on FPGA

Routing of connections between elements

Timing analysis to verify design meets requirements

6. Bitstream Generation
Generated programming file for FPGA

Verified no critical warnings during generation process

** Test Scenarios Verified**
Reset Condition: Elevator returns to floor 0 with doors open

Overweight Handling: Doors remain open when overweight signal is active

Floor Requests: Proper prioritization of floor requests

Movement Sequence: Correct incremental floor-to-floor movement

Door Operation: Proper opening/closing sequence

** Expected Results**
After reset: Floor = 0, Door = 1, Moving = 0

When request made: Door closes (Door = 0), then movement begins (Moving = 1)

During movement: Floor changes incrementally until destination reached

At destination: Movement stops (Moving = 0), doors open (Door = 1)
