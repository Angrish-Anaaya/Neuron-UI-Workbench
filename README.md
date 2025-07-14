# Neuron-UI-Workbench


A web-based graphical user interface for creating, configuring, and simulating small-to-medium-scale neural circuits. It combines an interactive React frontend with the powerful NEURON simulation engine on the backend, providing an intuitive "workbench" for computational neuroscience experiments.


Core Features

This application provides two distinct modes for circuit construction and simulation:

1. Individual Mode

A "hands-on" mode for building circuits neuron by neuron. Ideal for debugging, teaching, and understanding the interactions of a few cells.

Dynamic Circuit Manager: Add, remove, and rename individual neurons.

Interactive Schematic:

Click on a neuron to place a recording probe.

Click-and-drag probes along dendrites to change their position.

Click-and-drag from one neuron to another to create synaptic connections.

Click-and-drag connection endpoints to retarget synapses.

Detailed Configuration: Use sliders and checkboxes to configure the morphology (soma size, dendrite length/diameter) of each selected neuron.

Full-Featured Managers: Edit every parameter for connections, external stimuli (IClamp or Synaptic), and recording probes in detailed manager panels.

2. Probabilistic Mode

A high-level mode for defining and simulating large-scale networks based on a set of rules. Ideal for modeling circuits with hundreds or thousands of neurons.

Population-Based Modeling: Define distinct populations of neurons (e.g., "Excitatory," "Inhibitory") and set their quantity.

Connection Strategy Manager: Define rules for how populations connect to each other, specifying source/target, synapse type, and connection probability.

Stimulation & Recording Strategy Managers: Define rules for applying external stimuli to a percentage of a population and for placing recording probes on a random sample of cells.

Raster Plot Visualization: View the global network activity with a built-in raster plot that shows the spike time of every neuron in the simulation.


System Architecture

The application uses a standard client-server model:

Frontend (Client-Side): A React application built with Vite. It manages the UI and the entire circuit state. It sends the circuit definition as a single JSON object to the backend for simulation. All charts are rendered using Chart.js.

Backend (Server-Side): A lightweight Python server using the Flask web framework. Its sole purpose is to receive the JSON payload from the frontend, dynamically build the corresponding model in the NEURON simulation environment, run the simulation, and send the results (voltage traces and spike data) back to the frontend.


Data Flow for a Simulation:

User clicks "Run" → Frontend (React) sends JSON → Backend (Flask) receives JSON → Python script builds NEURON model → NEURON simulates → Backend sends results → Frontend displays graphs

How to Run the Application

To run this project, you will need two separate terminal windows.


Prerequisites

Python (3.8 or higher)

Node.js and npm

Setup Instructions


Clone the repository:

Generated bash
git clone https://github.com/your-username/Neuron-UI-Workbench.git
cd Neuron-UI-Workbench


Backend Setup (Terminal 1):

Navigate to the project's root directory.

Create and activate a Python virtual environment:

Generated bash
# For macOS/Linux
python3 -m venv .venv
source .venv/bin/activate

# For Windows
python -m venv .venv
.\.venv\Scripts\Activate
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Create a requirements.txt file in the root folder with the following content:

Generated code
Flask
Flask-CORS
neuron
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

Install the required packages:

Generated bash
pip install -r requirements.txt
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Frontend Setup (Terminal 2):

Navigate into the frontend subfolder:

Generated bash
cd frontend
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Install the required Node.js packages:

Generated bash
npm install
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END
Execution Instructions

Start the Backend: In Terminal 1 (with the Python venv activated), run the Flask server:

Generated bash
python server.py
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Leave this terminal running.

Start the Frontend: In Terminal 2 (inside the frontend folder), run the React development server:

Generated bash
npm run dev
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

View the Application: Open a web browser and navigate to the address provided by the frontend server (e.g., http://localhost:5173). The workbench UI should appear.

Code Structure

server.py: The complete backend server. It contains the Flask API endpoint /run_simulation and all the logic for dynamically building and running the NEURON model based on the received JSON payload.

frontend/src/App.jsx: The complete frontend application. This single React component manages all application state, UI rendering for both modes, and communication with the backend.

frontend/src/App.css: The complete stylesheet for the application, including the grid layout and styling for all UI components.
