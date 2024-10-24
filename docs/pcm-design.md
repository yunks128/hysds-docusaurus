# Processing Control and Data Management (PCM)

The Processing Control and Data Management (PCM) system is integral to managing and orchestrating jobs within the Hybrid Cloud Science Data System (HySDS). PCM controls all aspects of job distribution, scaling, and resource management across hybrid deployments involving both cloud services (e.g., AWS) and on-premise high-end computing platforms like NASA’s HECC.

## 1. **Components of PCM**

### Geospatial Region Query (GRQ)
GRQ is responsible for managing geospatial data through a faceted search system. It allows for the organization and cataloging of data, enabling the evaluation of production rules and the triggering of further jobs. GRQ plays a crucial role in ensuring that the correct data sets are processed based on user-defined rules.

Key functionalities include:
- **Faceted Search**: Manages large-scale geospatial data flowing through the system.
- **Rule-Based Triggers**: Allows automatic job submissions based on incoming data that match certain criteria, such as geospatial areas of interest.

### Verdi Workers
Verdi workers are the compute nodes responsible for running the processing jobs. These workers span both cloud and on-premise environments, supporting large-scale distributed processing.

Verdi's key roles:
- **Job Execution**: Runs Processing Geolocation Engine (PGE) containers on distributed nodes.
- **Auto-Scaling**: Verdi workers are dynamically scaled up or down based on workload demands, ensuring efficient resource use.
- **Hybrid Operation**: Supports job execution in both cloud (AWS) and on-premise (HECC) environments by using containers like Docker and Singularity.

### Mozart Job Management
Mozart handles the orchestration and management of jobs in PCM. It manages the queue of jobs and ensures that resources are allocated based on job priority and system capacity.

Mozart's functionalities include:
- **Job Queues**: Organizes jobs into type-specific queues and assigns them to available Verdi workers.
- **Auto-Scaling Groups (ASGs)**: Dynamically adjusts the number of Verdi workers based on the size of job queues to optimize performance and cost.
- **Fault Tolerance**: Retries failed jobs with higher priority based on failure conditions, such as timeouts.

## 2. **Hybrid Deployment and Scalability**

PCM is designed to operate across multiple environments, leveraging both cloud services and on-premise high-performance computing (HPC) resources.

### AWS and HECC Integration
The hybrid deployment involves running Verdi workers across AWS and HECC. This allows the system to utilize AWS's cloud scalability for lighter jobs while leveraging the computational power of HECC for more demanding tasks.

- **Unified PCM**: A single PCM cluster manages jobs spanning both AWS and HECC environments, ensuring seamless operation and data exchange between cloud and on-premise resources.
- **Data Sharing**: Data staging components handle data transfer between AWS and HECC, allowing jobs to move seamlessly across different infrastructures.

### Shared File Systems
A shared file system is used for data access across both on-premise and cloud environments. It facilitates the staging of data, allowing Verdi workers to access and process it regardless of whether the job is running on AWS or HECC.

- **Lustre File System**: On HECC, a Lustre shared file system is employed, ensuring that all compute nodes can access the same data, enhancing scalability and coordination between jobs.
- **Data Caching**: Data caching mechanisms are implemented to reduce the need for frequent data transfers between cloud and on-premise environments.

## 3. **Job Execution and Management**

The PCM leverages a combination of GRQ, Mozart, and Verdi workers to manage jobs from start to finish.

### Job Lifecycle:
- **Job Submission**: Jobs are submitted to PCM via faceted search triggers from GRQ or manually through job requests.
- **Queueing and Scaling**: Mozart places jobs into appropriate queues and triggers auto-scaling of Verdi workers based on queue size.
- **Execution**: Verdi workers execute the jobs, processing data and running algorithms.
- **Fault Tolerance**: In the event of failure, Mozart reassigns the job to another Verdi worker and retries with higher priority.

## Conclusion

The PCM provides a robust framework for managing large-scale distributed processing jobs across hybrid cloud environments. Its components, including GRQ, Verdi workers, and Mozart, work in concert to ensure scalability, fault tolerance, and efficient resource utilization across AWS and NASA's HECC infrastructure.
