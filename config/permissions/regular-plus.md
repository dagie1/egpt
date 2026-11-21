dangerously_skip_permissions: false

# config/permissions/regular-plus.md — LOCAL TIER on node dg (Dagiely 2026-11-01), for
# Queen D only. NOT `all`: the flag above is false, so brainpool.mjs's confinementFor
# confines her exactly like `regular` (file tools limited to her chat folder + her
# allowed_paths, --permission-mode default, no bare Bash, no bare Agent).
#
# What it adds over regular.md: a few SCOPED shell programs, pre-approved via
# --allowedTools, so she can download, install, clean and check the system when
# Dagiely orders or authorizes it (that rule lives in identities/queen-d.md; the
# node cannot ask Dagiely mid-turn). Every Bash entry is Bash(<bin>:*), never bare.
# curl is not path-gated: keeping downloads in media/ or Desktop/Queen D is her rule.
# She runs without admin rights (task egpt-daemon is Limited), so UAC installs and
# sfc/chkdsk /f cannot complete from here.
#
# Reachable only because permission-levels.mjs ACCESS_LEVELS lists 'regular-plus'
# (a local patch, like the daemon-runtime.mjs one). Parsed fresh every turn.

## Tools

- Read
- Write
- Edit
- Glob
- Grep
- WebSearch
- WebFetch
- Task
- Bash(/c/Users/DAGIELY/tools/queen-d/qbajar:*)    # download, ONLY into her media/ or Desktop/Queen D
- Bash(/c/Users/DAGIELY/tools/queen-d/qwinget:*)   # winget with fixed options only
- Bash(/c/Users/DAGIELY/tools/queen-d/qword:*)       # 2026-11-21 (Dagiely): read Word/Excel/PDF in her folders, create .docx (media/ + Desktop/Queen D)
- Bash(/c/Users/DAGIELY/tools/queen-d/qnavegador:*)  # 2026-11-21 (Dagiely): the browser, closed list of orders (tools/navegador/navegador.mjs)
# 2026-11-02: bare Bash(curl:*) and Bash(winget:*) REMOVED. Tested: `curl -o <path>` wrote
# outside her folders, and winget has --log / export -o / configure. Q must never be able to
# edit her own config, so only the two wrappers above (in a folder she cannot write) remain.
- Bash(systeminfo:*)   # check the system
- Bash(tasklist:*)     # running processes
- Bash(ipconfig:*)     # network
- Bash(ping:*)         # network
- Bash(df:*)           # free disk space
- Bash(du:*)           # folder sizes
- Bash(cleanmgr:*)     # Windows Disk Cleanup
# 2026-11-12: at this tier file tools are never pre-approved (claude-args.mjs FILE_TOOLS +
# --permission-mode default), so the bare Write/Edit above are denied everywhere (tested).
# These SCOPED rules pass through: she writes/edits ONLY in the media/ of the chat she is in
# (relative to the turn's cwd = the chat folder) and in her Desktop folder. Nothing else.
- Edit(./media/**)
# `?` stands for the space in "Queen D": permission-levels.mjs cuts a list item at its first
# whitespace, so a literal space here left a broken `Edit(//c/Users/DAGIELY/Desktop/Queen`.
- Edit(//c/Users/DAGIELY/Desktop/Queen?D/**)
