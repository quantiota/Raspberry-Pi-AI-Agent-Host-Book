# Frequently Asked Questions

1. **What is the AI Agent Host?**
   The AI Agent Host is a Dockerized environment designed for AI development. It's built on a modular system that allows different components to be added or removed based on the requirements of the project.

2. **Why use the AI Agent Host on a Raspberry Pi 4 8GB?**
   The AI Agent Host is lightweight yet powerful, making it suitable for the Raspberry Pi's limited hardware resources. It's designed to work with live data from both APIs and Raspberry Pi's own sensors, making it a powerful tool for real-time data analysis, modeling, and decision-making.

3. **Which services does the AI Agent Host include?**
   The AI Agent Host includes services such as Code-Server (a code editor), Grafana (a visualization tool), and QuestDB (a database). Additional services can be added or removed as needed.

4. **What do I need to connect to the Code-Server from a browser with HTTPS?**
   A fully qualified domain name (FQDN) is necessary to connect to the Code-Server from a browser using HTTPS. The FQDN ensures that the secure connection is correctly established.

5. **Can the AI Agent Host on a Raspberry Pi be used in combination with a remote JupyterHub installed on a GPU server?**

   Yes, this is one of the unique and powerful features of the AI Agent Host setup. You can use the AI Agent Host installed on a Raspberry Pi for real-time data analysis and decision making at the edge, while also connecting remotely to a JupyterHub installed on a GPU server for handling computationally intensive tasks. This innovative setup opens up new possibilities for AI development, especially in fields like IoT and edge computing.

6. **Can I use the AI Agent Host with other versions of the Raspberry Pi?**
   While the AI Agent Host has been tested and works well on the Raspberry Pi 4 8GB model, it should theoretically work on other models with sufficient hardware capabilities. However, performance may vary.

7. **Which operating systems are compatible with the AI Agent Host?**
   The AI Agent Host has been tested and found to be compatible with DietPi installed on a Raspberry Pi 4 8GB. Compatibility with other Linux distributions hasn't been extensively tested.

8. **Can I add my own services to the AI Agent Host?**
   Absolutely! The AI Agent Host is designed to be modular, allowing you to add or remove Docker containers as needed. This means you can customize the environment to include the exact tools and services that best suit your specific project's needs.

9. **What if I need help or support with the AI Agent Host?**
   There are active communities for both Raspberry Pi and AI Agent Host where you can expect robust support and resources for your AI development projects.
