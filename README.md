# Pure Storage API Snapshot Process
## We wanted to take Pure snapshots from clients in the most lightweight fashion possibly with no additional software.

The following scripts calls curl to communicate with the array

Requires curl, and networking connectivity between the client and the management interface on the array via https (443).

Authoriziation token is provided by storage array, either via API or GUI.

## Usage

A session must be created with a valid authorization sting.  The session command creates a cookie that can be used for subsequent commands.  The session cookie stays valid for 30 minutes, until it is explictly destroyed (via array command) or if the cookie file is deleted.

Once a valid session is established, any commands from the API reference can be run by specifying the cookie file.

### Snapshots

Snapshots cannot be presented to hosts in the Purity OS.  Instead, a snapshot is taken from a source device (or device group).

A target volume can then be refreshed from the snapshot.  The overwrite flag must be used to wipe out a volume that has been presented to a host and been in use.  Obviously make sure you have the correct target as the overwrite is immediate and not recoverable.  It may be adviseable to take a snapshot of the target device to roll back quickly should a mistake be made

Once the refresh is complete, the snapshot can be removed.  Leaving snapshots around will consume array space as source blocks change
