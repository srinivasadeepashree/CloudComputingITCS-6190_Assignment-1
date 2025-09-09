# CloudComputingITCS-6190_Assignment-1
Assignment #1: Docker Containers

## Overview
This project demonstrates a simple multi-container stack using Docker and Docker Compose. It consists of:  
- A **PostgreSQL database** container, initialized with a seeded table `trips`.  
- A **Python application** container that connects to the database, runs queries, computes basic statistics, outputs results as JSON to a file and prints them to the console.

This setup introduces fundamentals of containerized multi-service apps including service networking, environment variables, health checks, and reproducible workflows.

## Prerequisites
- Docker Desktop installed and running  
- Docker Compose  
- GitHub Desktop (for version control, optional)  
- An IDE or text editor (VS Code, PyCharm, etc.)  

Make sure you can run basic Docker commands.


## Repository Structure

 <img width="516" height="201" alt="Screenshot 2025-09-09 at 1 47 04 PM" src="https://github.com/user-attachments/assets/fd17d9da-c106-41fd-a965-4f713678b613" />


## Running the Stack

From the project root, create the output directory (if not exists):

>mkdir -p out

Build and start the stack with:

>docker compose up --build

Alternatively, use the Makefile for easier commands:

>make all

This will build images, start both containers, wait for the database to be ready, run the Python app, which connects to the database, performs queries, computes statistics, writes results to `out/summary.json`, and prints the summary JSON to the terminal.

## Output

The application writes its JSON summary output file to the out/ directory in the project root.

After running the stack, you will find the generated file at: out/summary.json

> { "total_trips": 6, "avg_fare_by_city": [
    {
      "city": "Charlotte",
      "avg_fare": 16.25
    },
    {
      "city": "New York",
      "avg_fare": 19.0
    },
    {
      "city": "San Francisco",
      "avg_fare": 20.25
    }
  ],
  "top_by_minutes": [
    {
      "city": "San Francisco",
      "minutes": 28,
      "fare": 29.3
    },
    {
      "city": "New York",
      "minutes": 26,
      "fare": 27.1
    },
    {
      "city": "Charlotte",
      "minutes": 21,
      "fare": 20.0
    },
    {
      "city": "Charlotte",
      "minutes": 12,
      "fare": 12.5
    },
    {
      "city": "San Francisco",
      "minutes": 11,
      "fare": 11.2
    },
    {
      "city": "New York",
      "minutes": 9,
      "fare": 10.9
    }
  ]
}

## Troubleshooting

- **DB not ready:** The app retries connecting multiple times; ensure the database container is healthy.  
- **Port conflicts:** Verify port 5432 is free or change PostgreSQL port in the Compose file.  
- **Permission issues:** Ensure the `out/` directory has write permissions for the app container.

## Cleaning Up

To stop and remove containers and volumes:

> make down
> 
