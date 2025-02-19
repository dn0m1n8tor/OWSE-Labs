
# Use Ubuntu 16.04 (Compatible with XAMPP & Atutor)
FROM ubuntu:16.04

# Set Environment Variables to Prevent Interactive Prompts
ENV DEBIAN_FRONTEND=noninteractive

# Update & Install Dependencies (Including `net-tools`)
RUN apt-get update && apt-get install -y \
    wget curl libaio1 libncurses5 unzip net-tools  # Add `net-tools`

# Create and switch to atutor-lab directory
WORKDIR /atutor-lab

# Download XAMPP and Atutor files and rename them properly
RUN wget -O xampp-installer.run "https://excellmedia.dl.sourceforge.net/project/xampp/XAMPP%20Linux/5.6.40/xampp-linux-x64-5.6.40-1-installer.run" && \
    wget -O Atutor.tar.gz "https://master.dl.sourceforge.net/project/atutor/atutor_2_2_1/ATutor-2.2.1.tar.gz"

# Install XAMPP (Includes PHP 5.6, Apache, and MySQL)
RUN chmod +x xampp-installer.run && \
    ./xampp-installer.run --mode unattended && \
    rm xampp-installer.run
    
# Copy Atutor to XAMPP's htdocs
RUN tar -xzf Atutor.tar.gz -C /opt/lampp/htdocs/ && \
    rm Atutor.tar.gz && \
    chmod -R 777 /opt/lampp/htdocs/ATutor

# Expose Port 80 (Apache) and 3306 (MySQL)
EXPOSE 80 3306

# Start XAMPP & Keep Container Running
CMD ["/bin/bash", "-c", "/opt/lampp/lampp start && tail -f /dev/null"]
