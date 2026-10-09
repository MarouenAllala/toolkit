# BPMN Toolkit

BPMN Toolkit is a software for designing and documenting business processes. You can:

- draw processes in BPMN, with subprocesses and called processes
- model business rules as DMN decision tables
- organise your work by product and application, with a version kept at every save
- export a process as BPMN XML, Kogito BPMN, SVG or a PDF documentation

It runs on your own machine or server, as a single jar.

---

## Installation

1. Install **Java 21** or later. Check it with:

   ```bash
   java -version
   ```

2. Put `bpmn-toolkit-version.jar` in a folder of its own. Your data and settings are stored in that folder. In the commands below, replace `version` with the version number in your jar's name.

3. Start it from that folder:

   ```bash
   java -jar bpmn-toolkit-version.jar
   ```

4. Open **http://localhost:8080** in your browser.


---

## Authentication

### Username and password

| | |
|---|---|
| Username | `admin` |
| Password | contact **mallala@dagitect.ch** |

The first time you sign in, you'll be asked to choose a new password. It needs at least 12 characters, with at least one letter and one digit.

After 5 wrong passwords in a row, sign-in is locked for 15 minutes.

The administrator adds other people from **Products → a product → Members Permissions → Add Member**.

### Microsoft Entra ID

You can also use **Sign in with Microsoft** with your work account. To get the configuration, contact **mallala@dagitect.ch**.

Microsoft sign-in only works if an administrator has already added you as a member with the same email address.

---

## Database

### SQLite (default)

Nothing to install or configure. On first start, BPMN Toolkit creates a file called `bpmn-toolkit.db` in the folder you started it from. That file holds all your data.

To back it up, stop the application, then copy the `.db` file.

### PostgreSQL

1. You need a PostgreSQL database and a user who can create tables in it. If you don't have one, you can start one with Docker:

   ```bash
   docker run -d --name bpmn-postgres \
     -e POSTGRES_DB=eventhub \
     -e POSTGRES_USER=eventhub \
     -e POSTGRES_PASSWORD=change-me \
     -p 5432:5432 \
     -v bpmn-postgres:/var/lib/postgresql/data \
     postgres:17
   ```

2. In the folder that contains the jar, create `config/application.yml`:

   ```
   my-folder/
   ├── bpmn-toolkit-version.jar
   └── config/
       └── application.yml
   ```

   with your database settings:

   ```yaml
   eventhub:
     database:
       type: postgresql
       postgresql:
         host: localhost
         port: 5432
         name: eventhub
         schema: public
         username: eventhub
         password: change-me
   ```

3. Start the jar from that folder as usual. The tables are created on first start.

You can also set these values with environment variables instead of the file: `EVENTHUB_DATABASE=postgresql`, `EVENTHUB_DB_HOST`, `EVENTHUB_DB_PORT`, `EVENTHUB_DB_NAME`, `EVENTHUB_DB_USERNAME` and `EVENTHUB_DB_PASSWORD`.

## License

### BPMN Toolkit

Copyright © 2026 Dagitect. All rights reserved.

BPMN Toolkit is proprietary software. You may not copy, modify, distribute or resell it without written permission. To ask for permission, contact **mallala@dagitect.ch**.

### Trademarks

BPMN™, Business Process Model and Notation™, DMN™ and Decision Model and Notation™ are trademarks of Object Management Group, Inc. BPMN Toolkit is not affiliated with, endorsed by or certified by OMG.

Microsoft and Microsoft Entra are trademarks of the Microsoft group of companies. PostgreSQL is a registered trademark of the PostgreSQL Community Association of Canada. Java is a registered trademark of Oracle and/or its affiliates. Docker is a registered trademark of Docker, Inc. Other names may be trademarks of their respective owners.
