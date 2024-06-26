# Hyrax_Apache_LDAP
## Overview
The **Opendap Protocol** (Open-source Project for a Network Data Access Protocol) is a crucial tool in the scientific field for sharing and accessing geospatial and scientific data distributed over networks. It standardizes data retrieval from various sources, allowing scientists to access and analyze information from different archives without full downloads. This enhances research development and collaboration among diverse teams and institutions, improving the efficiency and accuracy of scientific analyses.

**Hyrax** is a server application that implements the Opendap protocol. It offers a web interface for distributing scientific data, enabling users to query and retrieve data using Opendap via HTTP requests. Hyrax simplifies the publication and management of scientific data over networks, providing uniform and scalable access to datasets.

The **LDAP** (Lightweight Directory Access Protocol) is widely used for accessing and managing data stored within a directory service. It facilitates identity and permission management, allowing quick retrieval of information regarding users, groups, and other organizational entities. Its structural flexibility and ability to replicate data across multiple servers have made it a standard for centralized identity and resource management in complex networks.

Hyrax integrates sophisticated authentication via LDAP and resource access authorization with Apache. This synergy ensures precise data management, security, and adherence to access control policies. It allows for detailed control over who can access resources, providing a secure and compliant environment.

![Logic Diagram](https://github.com/fgr81/Hyrax_Apache_LDAP/blob/main/logic_diagram.png)

## How to use it 
0. ``` cp env.sample .env ```
1. Customize .env file
2. ``` docker-compose build ```
3. ``` docker network create custom-docker ```
4. ``` docker-compose up -d ```


[![DOI](https://zenodo.org/badge/819403840.svg)](https://zenodo.org/doi/10.5281/zenodo.12537436)
