# Setting up Origin on Windows

The Origin CLI has no native Windows build, so getting it working means going through WSL.
A real setup hits four walls on the way: the WSL install itself, filesystem metadata on
`/mnt/c`, a missing git identity, and the CLI landing off PATH. This guide covers them in
the order you hit them.

Tested 2026-08-20 on a clean Windows machine.

## There is no native Windows build

The official docs list macOS, Linux, and Windows via WSL. There is no native Windows
install, so the first step is a Linux distro:

```powershell
wsl --install -d Ubuntu
```

Run that from an elevated PowerShell. A Windows restart may be required, though not if the
WSL engine is already installed for something else.

Having WSL installed for something else does not mean a usable distro exists. Check what is
actually there:

```powershell
wsl -l -v
```

A `docker-desktop` entry is not a usable distro.

On first launch of Ubuntu you create a Linux username and password. They are separate from
your Windows account, and the password does not echo while you type it.

## Metadata on /mnt/c

If your repos live on the Windows filesystem under `/mnt/c`, enable metadata support. What
it does is store Linux ownership and mode bits in NTFS extended attributes, which is what
silences the `chmod` noise on push and keeps permission bits sane.

Separately, and worth being precise about: on one machine I hit a symptom where
`git branch --set-upstream-to` printed its success message and saved nothing, and the next
command that needed the upstream reported there was no tracking information for the branch.

I could not reproduce that symptom on a second clean machine with metadata off. Git config
wrote and read back fine, and branch tracking saved correctly. So metadata being the cause
of that symptom is **unconfirmed**, and repo-level git config writes on `/mnt/c` are not
something I can say fail without it.

If you do see the symptom, do not trust the success message. Read the setting back at the
repo level:

```bash
BRANCH=$(git branch --show-current)
git config --get branch.$BRANCH.remote
git config --get branch.$BRANCH.merge
```

Both reads print nothing if the write did not land. `git branch -vv` is the quicker
summary view of the same thing. Also check whether metadata is on at all.

To enable it, edit the WSL config:

```bash
sudo nano /etc/wsl.conf
```

Add an `[automount]` section:

```ini
[automount]
options = "metadata"
```

If the file already has other sections such as `[boot]` or `[user]`, add `[automount]` as
its own section rather than replacing the file. If `[automount]` is already there, add
`metadata` to its existing `options` value rather than adding a second section.

Then restart WSL from PowerShell, reopen Ubuntu, and check the mount:

```powershell
wsl --shutdown
```

```bash
mount | grep "C:"
```

Look for `metadata` in the output.

## A fresh WSL has no git identity

Nothing carries over from Windows. The first commit fails with "Author identity unknown."
Set both values:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## The CLI installs off PATH

Install the CLI:

```bash
curl -fsSL https://downloads.cursor.com/origin/install.sh | sh
```

It installs to `~/.local/bin`, which is not on PATH. The installer prints a note about
this, but it is easy to miss, and `origin --version` then fails with `command not found`.

The note suggests a bare `export`, which does not survive closing the terminal. Make it
durable instead:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Then verify:

```bash
origin --version
```

## Authenticating

```bash
origin auth login
```

This opens a browser flow. On success it automatically configures the git credential helper
for `origin.cursor.com`. Cloning and pushing then work normally.

## Gotchas

| Thing | Detail |
|---|---|
| Native Windows build | There is none. Docs list macOS, Linux, and Windows via WSL |
| `wsl --install` | Needs an elevated PowerShell. A restart may be required |
| Existing WSL | Not the same as a usable distro. Check `wsl -l -v`; `docker-desktop` is not one |
| Linux password | Separate from your Windows account, and it does not echo while typing |
| Metadata on `/mnt/c` | Worth enabling: keeps ownership and mode bits sane, silences `chmod` noise |
| The upstream symptom | Seen once, not reproducible with metadata off. Cause unconfirmed |
| Git identity | Not set in a fresh WSL. The first commit fails until it is |
| CLI on PATH | Installs to `~/.local/bin`. Put the `export` in `~/.bashrc`, not just the shell |
| Credential helper | `origin auth login` configures it for `origin.cursor.com` on success |

## Notes

Origin is in early beta and this behavior may change. Everything above was verified
firsthand on a clean Windows machine on 2026-08-20, with one exception called out in place:
the upstream symptom under "Metadata on /mnt/c" did not reproduce, and its cause is
unconfirmed.
