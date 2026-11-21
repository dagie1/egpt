dangerously_skip_permissions: false

# config/permissions/regular-word.md — LOCAL TIER on node dg (Dagiely 2026-11-12), for
# Judge D only. Exactly regular.md (the flag above is false, so brainpool.mjs's confinementFor
# confines her: file tools limited to her chat folder + her allowed_paths, no bare Bash, no bare
# Agent) plus ONE scoped program, pre-approved via --allowedTools:
#
#   jword leer <ruta.docx|ruta.doc> [parte]    read a Word file, by parts
#   jword crear <borrador.md> <nombre.docx>    create a .docx from a draft in her chat
#
# jword drives Dagiely's Word 2010 invisibly (macros force-disabled). It reads only inside her
# allowed_paths, Desktop/Judge D and her current chat, writing nothing there; it writes only
# into her chat's desktop/ and Desktop/Judge D, never overwriting. It lives in
# C:/Users/DAGIELY/tools/judge-d, a folder she cannot write. Copies: .egpt/local/judge-d-tools.
#
# Reachable only because permission-levels.mjs ACCESS_LEVELS lists 'regular-word'
# (a local patch, like 'regular-plus'). Parsed fresh every turn.

## Tools

- Read
- Write
- Edit
- Glob
- Grep
- WebSearch
- WebFetch
- Task
- Bash(/c/Users/DAGIELY/tools/judge-d/jword:*)   # Word: read .docx/.doc, create .docx
- Bash(/c/Users/DAGIELY/tools/judge-d/jbajar:*)  # 2026-11-12: download, ONLY into her chat's desktop/ or Desktop/Judge D
- Bash(/c/Users/DAGIELY/tools/judge-d/jnavegador:*)  # 2026-11-21 (Dagiely): the browser, closed list of orders (tools/navegador/navegador.mjs)
# 2026-11-12: at this tier file tools are never pre-approved (claude-args.mjs FILE_TOOLS +
# --permission-mode default), so a bare Write is denied everywhere ("you haven't granted it
# yet"). This SCOPED rule passes through and lets her write/edit ONLY in the desktop/ of the
# chat she is in (relative to the turn's cwd = the chat folder): her drafts for jword crear.
- Edit(./desktop/**)
