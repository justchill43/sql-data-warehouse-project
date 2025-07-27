FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive
ENV ACCEPT_EULA=Y
ENV SA_PASSWORD=YourStrong!Passw0rd
ENV MSSQL_PID=Express

# Install required packages
RUN apt-get update && apt-get install -y curl gnupg2 software-properties-common apt-transport-https wget

# Microsoft SQL Server repo keys & list
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/ubuntu/20.04/mssql-server-2019.list | tee /etc/apt/sources.list.d/mssql-server.list && \
    curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list | tee /etc/apt/sources.list.d/msprod.list

# Install SQL Server and command-line tools
RUN apt-get update && \
    apt-get install -y mssql-server mssql-tools unixodbc-dev && \
    apt-get clean && \
    echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc

# Add mssql-tools to system PATH
ENV PATH="/opt/mssql-tools/bin:$PATH"

# Set up SQL Server (will complete on run)
RUN /opt/mssql/bin/mssql-conf -n setup accept-eula

# Expose SQL Server default port
EXPOSE 1433

# Start SQL Server
CMD ["/opt/mssql/bin/sqlservr"]
