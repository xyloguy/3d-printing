# Slicer Settings

--------------------

## CURA Settings

#### Start G-code

```
; --- Global Settings
; layer_height = {layer_height}
; smooth_spiralized_contours = {smooth_spiralized_contours}
; magic_mesh_surface_mode = {magic_mesh_surface_mode}
; machine_extruder_count = {machine_extruder_count}
; --- Single Extruder Settings
; speed_z_hop = {speed_z_hop}
; retraction_amount = {retraction_amount}
; retraction_hop = {retraction_hop}
; retraction_hop_enabled = {retraction_hop_enabled}
; retraction_enable = {retraction_enable}
; retraction_speed = {retraction_speed}
; retraction_retract_speed = {retraction_retract_speed}
; retraction_prime_speed = {retraction_prime_speed}
; speed_travel = {speed_travel}

; Ender 3 Custom Start G-code
M140 S{material_bed_temperature} ; start heating bed
M104 S160 ; start warming extruder
G28 ; Home all axes
M190 S{material_bed_temperature} ; wait for heat bed temp
G29 ; Auto bed-level (BL-touch)
G92 E0 ; Reset Extruder
M104 S{material_print_temperature} ; start heating extruder
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X0.1 Y20 Z0.3 F5000.0 ; Move to start position
M109 S{material_print_temperature}; wait for extruder temp
G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; Draw the first line
G1 X0.4 Y200.0 Z0.3 F5000.0 ; Move to side a little
G1 X0.4 Y20 Z0.3 F1500.0 E30 ; Draw the second line
G92 E0 ; Reset Extruder
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
; End of custom start GCode
```

#### End G-code

```
; Ender 3 Custom End G-code
M400 ; Wait for current moves to finish
M220 S100 ; Reset Speed factor override percentage to default (100%)
M221 S100 ; Reset Extrude factor override percentage to default (100%)
G91 ; Set coordinates to relative
G1 F2700 E-2 ; Retract filament 3mm at 40mm/s to prevent stringing
G0 F5000 Z20 ; Move Z Axis up 20mm to allow filament ooze freely
G90 ; Set coordinates to absolute
G0 X0 Y235 F5000 ; Move Heat Bed to the front for easy print removal
M106 S0 ; turn off fan
M104 S0 ; turn off extruder temperature
M140 S0 ; turn off heated bed
M84 X Y E; Disable stepper motors (except Z)
; End of custom end GCode
```

--------------------

## PrusaSlicer Settings

#### Start G-code (ABL)

```
; Ender 3 Custom Start G-code
M140 S[first_layer_bed_temperature] ; Set Heat Bed temperature
M104 S160; start warming extruder to 160
G28 ; Home all axes
M190 S[first_layer_bed_temperature] ; Wait for Heat Bed temperature
G29 ; Auto bed-level (BL-Touch)
G92 E0 ; Reset Extruder
M104 S[first_layer_temperature] ; Set Extruder temperature
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X0.1 Y20 Z0.3 F5000.0 ; Move to start position
M109 S[first_layer_temperature] ; Wait for Extruder temperature
G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; Draw the first line
G1 X0.4 Y200.0 Z0.3 F5000.0 ; Move to side a little
G1 X0.4 Y20 Z0.3 F1500.0 E30 ; Draw the second line
G92 E0 ; Reset Extruder
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
; End of custom start GCode
```

#### End G-code (ABL)

```
; Ender 3 Custom End G-code
M400 ; Wait for current moves to finish
M220 S100 ; Reset Speed factor override percentage to default (100%)
M221 S100 ; Reset Extrude factor override percentage to default (100%)
G91 ; Set coordinates to relative
G1 F2700 E-2 ; Retract filament 3mm at 40mm/s to prevent stringing
G0 F5000 Z20 ; Move Z Axis up 20mm to allow filament ooze freely
G90 ; Set coordinates to absolute
G0 X0 Y235 F5000 ; Move Heat Bed to the front for easy print removal
M106 S0 ; turn off fan
M104 S0 ; turn off extruder temperature
M140 S0 ; turn off heated bed
M84 X Y E; Disable stepper motors (except Z)
; End of custom end GCode
```
