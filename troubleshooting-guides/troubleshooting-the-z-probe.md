# Troubleshooting the Z-probe

This guide will cover various problems that you might encounter while working with the Z-probe.

## Error: Z-probe Triggered Before Move

![](../.gitbook/assets/errorzprobetriggeredbefore.png)

### Problem

The probing procedure does not start and the Error: Z-probe Triggered Before Move is  printed in the console.

### Explanation

This indicates that the firmware has detected a triggering Z-probe value before it has even started moving the Z-platform. This can be seen in the _Machine Status_ table as the _Z-probe_ value will usually be 1000. The procedure here is attempting to move the Z-platform to the Z-probe in order to trigger it, but the Z-probe is already triggered.

### Solution

1. Test that the Z-probe value in the Duet Web Console is toggling correctly.
2. Ensure that the Z-probe is properly connected.
3. Ensure that the Z-probe is properly configured with the `M558` command.

## Error: Z-probe Not Triggered During Move

![](../.gitbook/assets/errorzprobenottriggered.png)

### Problem

As the image above indicates, the Error: Z-probe Not Triggered During Move is printed out and the probing operation has failed. If the printer was moving during the probing command, the printer stopped moving before the Z-probe was triggered.

### Explanation

This error is actually a fail safe, the printer is preventing what it presumes is a crash. Since the printer does not know where the mechanical limits of the printer are, it assumes the software limits are the limits of its motion. When the printer is performing its probing procedure it reaches the axes limit before the Z-probe is triggered and prints the error above.  

### Solution

1. Disable axes limits with the command `M564 S0`
2. Make sure that the Z-probe value on the Duet Web Console changes when the Z-probe is supposed to be triggered.
3. Ensure that the printer never reaches a value less than 0 in the Z, during a probe move. You can do this by sending the command `G92 Z50` while the printer is less than 50mm away from the nozzle. **Warning: Travelling to a small Z-value after you do this will crash the printer!**

