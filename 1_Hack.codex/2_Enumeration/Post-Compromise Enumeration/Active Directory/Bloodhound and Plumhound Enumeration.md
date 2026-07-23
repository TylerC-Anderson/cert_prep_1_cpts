
## Quick-Use

**Commands**:
- To run bloodhound:
    - **Current Kali (2025.2+):** the `neo4j console` → `sudo bloodhound` flow below is deprecated (`bloodhound` is now BloodHound CE, native — not Docker). Run `sudo bloodhound-setup` once (inits neo4j + postgres), then `bloodhound-start`. Web UI at http://localhost:8080, first login `admin`/`admin` (forced change). `bloodhound-stop` to shut down.
    - *Legacy (course-era) flow below:*
    - `sudo neo4j console`
        - navigate to http://localhost:7474/ (or whichever portnum given by the CLI output after putting in the above command)
    - back in CLI `sudo bloodhound`
        - login to webconsole with neo4j:neo4j (or the appropriate password if you've logged in before)
    - to setup an ingester: `sudo bloodhound-ce-python -d ADNAME -u uname -p Password -ns TARGIPADDR -c all`
        - ⚠️ use `bloodhound-ce-python` (Kali package of the same name), **not** the legacy `bloodhound-python` — the old ingestor's output will not load into BloodHound CE
        - back in bloodhound webconsole, `Upload Data` -> import the data you collected with the ingester

- To run Plumhound, you NEED bloodhound run from above:
    - to init: `sudo python3 PlumHound.py --easy -p BloodhoundPassword`
    - then: `sudo python3 PlumHound.py -x tasks/default.tasks -p BloodhoundPassword`

*Tools*:
- 

## General

**Objectives**:
While within the Bloodhound webconsole, you can:
- discover paths to high value targets
- Mark users/machines as owned
- find Roastable services
- See all flags for users and policies
- See map of Domain and Trees
- much more

**Overview**:

## Glossary
