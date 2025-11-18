# Skill Story Database Container

Purpose:
- Provide a PostgreSQL database for the Skill Story LMS.
- Initialize the database, user, and permissions.
- Optionally write a connection helper and env file for external tools.

What this container does NOT do:
- It does not run any Node.js or Express applications.
- It does not install Node dependencies during its build.
- Frontend/backend containers (or the host) are responsible for Node/Express.

Startup:
- startup.sh starts PostgreSQL only and applies minimal initialization.
- A convenience file db_connection.txt is created with a psql URL.
- A convenience env file db_visualizer/postgres.env is created for optional external tools.

Optional tools:
- The db_visualizer directory contains an optional Node-based viewer for local debugging. Do not run it in this container. If needed, run it from your host or a separate utility container:
  - cd db_visualizer
  - npm install
  - source ./postgres.env
  - npm start

Security:
- No secrets are hardcoded for production. For real deployments, use environment variables or secret managers.
- Do not expose any diagnostic viewer publicly.

