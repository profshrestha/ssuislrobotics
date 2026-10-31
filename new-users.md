# Instructions for new users

[Back to the index](README.md)

## Your account

**Your username is your SSU user id,** the part of your campus address before the `@`. Someone
whose address is `doej@sonoma.edu` has the username `doej` on every lab machine.

**A one-time password is issued when the account is created.** It is set to expire immediately,
so the first login asks you to choose a new one before the session begins. Choose something you
have not used elsewhere.

Accounts carry no administrative privileges. Everything described in [Software](software.md) is
already installed, and nothing in the course or research work requires installing software
system-wide.

## Your account is local to each machine

This is the point that most often surprises people, so it is worth stating plainly.

The ten workstations run the same image and look identical, but **each machine keeps its own
accounts and its own home directories.** There is no shared file server and no network home
directory. An account on station III and an account on station IX share a username and nothing
else.

Three consequences follow:

- **Your files do not follow you.** Work saved on one machine is on that machine only.
- **Your password does not follow you either.** Changing it on one station changes it there
  alone. If you have accounts on several machines, each has its own password.
- **A file you cannot find is usually on another station.** Check which machine you were sitting
  at before concluding that anything was lost.

## Working across several machines

If your work takes you to more than one station, keep the work somewhere that travels:

- **A Git repository** is the better option. Commit and push before you leave a station, and pull
  when you sit down at the next one. This also gives you a history and a copy that survives the
  end of the semester.
- **A USB drive** works for data that does not belong in version control, such as camera
  recordings or large datasets.

Copying files between stations over the network is not set up for general use. Use one of the two
options above.

## Your home directory is private

Home directories are readable only by their owner. Other users on the same machine cannot read
your files, and you cannot read theirs.

That privacy depends on your own care as well. Before committing anything to a repository, run
`git status` and look at what is staged. Credentials, tokens, and `.env` files are never
committed.

If you log in to any tool at a station, log out when you leave. The machines are shared, and a
session left open is a session someone else inherits.

## Ending a session

**Log out, and leave the machine powered on.**

Logging out ends your session and protects your files while leaving the machine running. The
stations are maintained and updated remotely, and one that has been powered off is unreachable:
it misses that maintenance, and the next person finds it in a state nobody intended. Leave the
station at the login screen.

## Accounts last one semester

**Access is granted for a single semester.** At the conclusion of the semester, lab accounts and
everything in them are deleted. This includes home directories, saved work, configuration, and
any data left on the machine.

This is not a quota or an archive policy. Nothing is retained, and nothing can be recovered
afterwards.

**Back up anything you want to keep before the semester ends.** A Git repository under your own
account is the straightforward way to do this, and a USB copy is a reasonable addition for
material that does not belong in version control. If you expect to continue into the following
semester, request a new account rather than assuming the existing one persists.

## Working with the manipulators

Read [Machine and robot hardware](hardware.md) before handling an arm. Two rules apply in every
case:

- **Fix the base before applying power,** and clear the full reach of the arm of laptops,
  bottles, cables, and hands.
- **Stay within reach of the power disconnect** when commanding motion for the first time. If an
  arm moves toward the work surface, disconnect power rather than intervening by hand.

The WidowX AI is heavier and faster than the RX150, and a sign error in a commanded pose carries
correspondingly greater consequences. Verify a configuration in visualization before sending it
to hardware.

## Getting help

For account problems, access requests, and anything concerning the hardware, contact the lab
director. For a problem with a specific machine, note which station you were at: the hostname is
shown at the login screen and is returned by `hostnamectl --static`.
