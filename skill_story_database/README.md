# Skill Story Database Container

Purpose:
- Provide a PostgreSQL database for the Skill Story LMS.
- Initialize the database, user, and permissions.
- Optionally write a connection helper and env file for external tools.

What this container does NOT do:
- It does not run any Node.js or Express applications.
- It does not install Node dependencies during its build.
- Frontend/backend containers (or the host) are responsible for Node/Express.
- The optional db_visualizer is NOT started from this container and must be run externally.

Startup:
- startup.sh starts PostgreSQL only and applies minimal initialization.
- A convenience file db_connection.txt is created with a psql URL.
- A convenience env file db_visualizer/postgres.env is created for optional external tools.
- Guard: This container must never invoke `node server.js` or `npm start`. Ensure Dockerfile CMD/ENTRYPOINT only runs Postgres (via startup.sh).

Optional tools (External Only):
- The db_visualizer directory contains an optional Node-based viewer for local debugging. Do not run it in this container.
- To use it (on host or separate utility container):
  1) cd skill_story_database/db_visualizer
  2) npm install
  3) source ./postgres.env
  4) npm start
  5) Open http://localhost:3000

Security:
- No secrets are hardcoded for production. For real deployments, use environment variables or secret managers.
- Do not expose any diagnostic viewer publicly.
