## How to install BloodHound Legacy in Linux

### Download the BloodHound Legacy 

```
wget https://github.com/SpecterOps/BloodHound-Legacy/releases/download/v4.3.1/BloodHound-linux-x64.zip
```
#### Unzip the BloodHound Legacy

```
unzip BloodHound-linux-x64.zip
```

#### Change directory to the BloodHound Legacy Folder

```
cd BloodHound-linux-x64
```

### Create docker-compose.yml

```
version: '3.8'

services:
  neo4j:
    image: neo4j:4.4
    container_name: bloodhound-neo4j
    environment:
      - NEO4J_AUTH=neo4j/BloodHound
      - NEO4JLABS_PLUGINS=["apoc"]
      - NEO4J_dbms_security_procedures_unrestricted=apoc.\\\*
    volumes:
      - neo4j_data:/data
      - neo4j_logs:/logs
      - neo4j_import:/var/lib/neo4j/import
    ports:
      - "7474:7474"
      - "7687:7687"
    restart: unless-stopped

volumes:
  neo4j_data:
  neo4j_logs:
  neo4j_import:

```


### Run the docker compose

```
docker compose up
```

### Run the BloodHound Legacy 

```
./BloodHound --no-sandbox
```

### Credential of neo4j

```
neo4j:BloodHound
```
