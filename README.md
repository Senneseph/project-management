# op — OpenProject CLI

Lightweight Perl CLI for the [OpenProject](https://www.openproject.org/) REST API (v3). Zero non-core Perl dependencies.

## Example Usage

```bash
tools/op help                      # show help
tools/op project list              # list all projects
tools/op project create "Neo-Mach" neo-mach
tools/op project get <id|slug>
tools/op project update 3 name="New Name"
tools/op project delete <id|slug>

tools/op wp list                   # list tickets in default project
tools/op wp list --status New --priority High
tools/op wp list --project gnu-mach-hurd
tools/op wp create "Port USB stack" --type Milestone --priority High
tools/op wp create "Subtask" --type Task --parent 42
tools/op wp link 42 --precedes 43   # 42 must finish before 43 starts
tools/op wp update 42 status="In progress" subject="Updated"
tools/op wp delete 42
tools/op wp types|statuses|priorities   # reference data

tools/op board list                 # list boards in the project
tools/op board summary              # Kanban overview: columns, counts,
                                    #   open/closed, types, hot items
tools/op board summary 11           # specific board by id or name
tools/op board summary --project neo-mach

tools/op config                    # show active .env settings
```

## Configuration

Read from `.env` in the project root:

| Variable | Purpose |
|---|---|
| `OPENPROJECT_URL` | Server base URL (e.g. `http://localhost:8080`) |
| `OPENPROJECT_ACCESS_TOKEN` | Bearer token |
| `OPENPROJECT_USERNAME` | Display user |
| `OPENPROJECT_PROJECT_ID` | Default target project for `wp` commands |

Override the default project with `--project <id|slug>` on any `wp` subcommand.

## Dependencies

Only core Perl modules (v5.28+): `LWP::UserAgent`, `HTTP::Request`, `JSON::PP`, `Getopt::Long`. No CPAN installs needed.
