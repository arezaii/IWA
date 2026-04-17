# MyCM Sale Setup Summary

This document is intended to function as an operations handoff for preparing and launching a MyCM sale with a networked POS setup.

Source documents reviewed:

- Manual-Owner Activate Sale-Rev17-01-14-19-SUPPORT-2.txt
- Manual-Owner Manage Sale-Rev35.txt
- PresaleTrial-POS614b30-Offline-FULL-Manual3-PresaleOnly-10-06-2024.txt
- PresaleTrial-POS6-Network-Manual3-03-05-24-ApppendicesOnly.txt

Operational scope:

- owner-side event preparation
- loading the event file
- setting up the master POS
- setting up multiple satellite POS machines
- important notes for a networked deployment

## Access Codes

- POS Email Receipts Access Code: `ePassUTob`
- POS Synchronize Data Access Code: `sPassG97Y`
- POS Event Transaction Fees Access Code: `txnfee235UxN`

## Important Limitation

This handoff combines guidance from the main owner manuals, the offline POS manual, and the network appendices.

A true networked setup requires:

- the MyCM POS Network version
- a server/master
- a router or intranet
- MyCM approval to use the network version

Some network features are still only partially documented. Suspend / Pay Station is identified as available, but the detailed appendix procedure is not included in the available text. Treat that feature as supported but not fully documented in this handoff.

## Operating Sequence

Use this as the working order of operations:

1. Activate the event online.
2. Let sellers register and enter items.
3. Choose the registration close date early enough to give yourself time to load the event into POS before the event.
4. Lock the event or otherwise mark items downloaded before final POS setup.
5. Install and configure the POS systems.
6. In network mode, start the server first and then open the master POS.
7. Load the event file into the master first.
8. Configure the master completely before bringing satellite machines online.
9. For network mode, connect all stations through the server/master and intranet.
10. Test checkout flow before the live event.
11. Keep backups and verify them throughout the event.

## Owner-Side Preparation

Complete these items before touching the POS machines:

- Finish event activation.
- Confirm tag format and sale settings.
- Let sellers complete registration and item entry.
- Pick a registration end date that gives you enough buffer before sale day.
- Plan to download the event file on or after the registration end date, before the event opens.

Do not set the registration close date too late. You need enough time after registration closes to lock the event, load the event file, validate the master, and test the stations before opening day.

## Hardware and Environment Guidance

Build the environment around the master machine.

- Use the strongest computer as the master.
- The master is expected to act as both the master and Register 1.
- If using multiple computers, each additional station must have a unique register identity.
- Never configure two machines with the same register name.
- Do not wait until the last minute; the manuals recommend having systems ready at least 16 hours before opening.

For network mode specifically:

- You need the network-enabled MyCM POS setup, not just the offline version.
- You need a server/master and a router or intranet.
- The manuals indicate MyCM approval is required for the POS Network version.
- Start the server first, then open the master POS.
- The master network setup uses the network register mode and requires the network password `mycm-net`.

## Event File Loading Guidance

Always load the event file into the master first.

Master event-file loading sequence:

1. Install the correct POS version on all machines.
2. In network mode, double-click the Start Server icon first and let it finish.
3. Open the master and configure it as `Master`.
4. Choose the network register mode and enter the network password.
5. Browse to `http://localhost:8080/mycmpos`, get the correct IP address, and enter that IP into the confirmation screen.
6. Reopen the POS and load the event file only into the master first.
7. Do not load the event file into the other machines until the master is fully configured.

During the first event-file load, use these choices unless you have a documented reason to do otherwise:

- Download all items on the first full load.
- Choose `Yes` to mark items as downloaded.
- Choose `Yes` to lock the event if you want maximum consistency between online data and POS data.

Operational reason:

- It protects data integrity.
- It prevents sellers from editing or deleting already-loaded items.
- It reduces mismatch risk between website data and POS data.
- It is important for accurate sell-through reporting.

## Master POS Setup

Once the event file is on the master, finish the master before moving to any other station:

1. Set program passwords immediately.
2. Review event setup values on the master.
3. Verify tax, discount, and any event-specific defaults.
4. Complete the master configuration before touching the other registers.

The master is responsible for:

- holding the complete event data
- driving settings and preferences
- generating end-of-night reports
- generating final settlement reports
- carrying the aggregate data for all other stations

Treat the master as the system of record for the event.

## Satellite POS Setup

The detailed satellite instructions in the offline manual are written for the offline workflow. In that model, satellites inherit master settings through a master-to-register export file.

The parts that still apply operationally are:

- configure the master first
- give each station a unique register name
- make each satellite inherit the master's configuration rather than configuring each one independently
- never duplicate register names

Offline reference process:

1. Create a `Master to Register Export` from the master.
2. Move that export to the next register.
3. Import it on the satellite machine.
4. Repeat for Register 2, Register 3, and so on.

For a networked deployment, use that as the control model, not necessarily the literal procedure.

In network mode, the intended operating model is:

- the master/server is still the source of truth
- each station still needs a unique identity
- stations should inherit the master/server-backed configuration
- some of the offline memory-stick export/import workflow is replaced by the network/server setup flow

The network quick guide also makes these setup expectations explicit:

- insert the memory stick for each computer before starting setup
- start the server first
- open the master first
- configure the master before the other stations
- run a test transaction on the master after loading the event file

## Networked Sale Guidance

Use these assumptions when staffing and configuring a networked event:

- The network version supports scan stations and separate pay stations.
- Suspended transactions from scan stations can be resumed later at pay stations.
- This setup can reduce the number of money-handling stations.
- It can speed lines and simplify worker roles.

The available documents also give two concrete network setup details:

- the master startup sequence is `Start Server` first, then open the master POS
- if automatic event download is not available, Appendix N documents manual event-file download and manual loading into the master

Recommended operating plan for a networked sale:

1. Confirm you are approved for and using the MyCM POS Network version.
2. Build the environment around one server/master and a functioning router/intranet.
3. Configure the master first and verify the event file is correct there.
4. Bring each satellite POS online with a unique register identity.
5. Use scan stations and pay stations intentionally if that fits your staffing plan.
6. Do not rely on the offline nightly import flow if your stations are truly network-connected.

## Manual Event File Fallback

If automatic event-file download is unavailable, use this fallback:

1. Make sure the event is locked.
2. Download the event file from the owner portal.
3. Save it to the Event File folder on `C:/mycmposv6.x/Event File` or on the memory stick in `mycmposv6/Event File`.
4. On the master only, use `Download the Event File Manually` and browse to that saved event file.

This is the documented fallback if the normal automatic master download is unavailable.

## What Still Applies From the Offline Manuals

Even in a networked event, keep these operating rules in force:

- never use duplicate register names
- never re-download the event file in the middle of the event on a machine already in use
- do not delete or move MyCM folders once the event setup is complete
- set antivirus or security exception folders correctly
- keep backups current and verify they are actually being written

## Recommended Practical Setup Sequence

Use this as the pre-event setup checklist:

1. Activate and finalize the event online.
2. Let sellers finish registration and item entry.
3. Close registration with enough lead time.
4. Lock the event or mark items downloaded before final POS rollout.
5. Confirm with MyCM that your event is using the Network POS version.
6. Prepare the server/master and router/intranet.
7. Install the correct POS version on all computers.
8. Insert each computer's memory stick before starting setup.
9. Start the server on the master machine.
10. Configure the strongest machine as `Master` in network mode.
11. Load the event file into the master first.
12. Set passwords and verify event settings on the master.
13. Run a test transaction on the master to confirm inventory loaded correctly.
14. Bring each satellite station online one at a time with unique register names.
15. Validate that each station is connected and functioning before sale day.
16. Test your actual checkout flow using the network model you plan to use on event day.
17. Verify backups and keep monitoring them during the event.

## Operational Model for Your Networked Sale

For planning purposes, treat the event as operating like this:

- The master/server remains the central control point.
- The networked stations should not be treated like independent offline registers that require manual nightly consolidation.
- Network mode is meant to support connected scan and pay workflows.
- The offline manual is still useful for master-first setup discipline, register naming, data-integrity choices, and operational cautions.
- The network appendices provide a startup sequence for the master and a documented manual event-file fallback.

## Recommended Next Step

Before final rollout, obtain any additional MyCM network-specific instructions that cover full station onboarding and pay-station behavior in more detail. That is the main remaining gap between this handoff and a complete field procedure.
