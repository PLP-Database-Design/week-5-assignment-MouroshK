QUESTION 1

const express = require('express');
const mongoose = require('mongoose');

// Create an Express app
const app = express();

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/hospital', { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log("Connected to MongoDB"))
  .catch((err) => console.log("Failed to connect to MongoDB", err));

// Define the Patient schema
const patientSchema = new mongoose.Schema({
  patient_id: { type: Number, required: true },
  first_name: { type: String, required: true },
  last_name: { type: String, required: true },
  date_of_birth: { type: Date, required: true }
});

// Create the Patient model
const Patient = mongoose.model('Patient', patientSchema);

// Define the GET endpoint to retrieve all patients
app.get('/patients', async (req, res) => {
  try {
    const patients = await Patient.find(); // Retrieve all patients from the database
    res.json(patients); // Send the patient data as JSON
  } catch (err) {
    res.status(500).json({ message: "Error retrieving patients" });
  }
});

// Start the server on port 3000
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});


QUESTION 2

const express = require('express');
const mongoose = require('mongoose');

// Create an Express app
const app = express();

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/healthcare', { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log("Connected to MongoDB"))
  .catch((err) => console.log("Failed to connect to MongoDB", err));

// Define the Provider schema
const providerSchema = new mongoose.Schema({
  first_name: { type: String, required: true },
  last_name: { type: String, required: true },
  provider_specialty: { type: String, required: true },
});

// Create the Provider model
const Provider = mongoose.model('Provider', providerSchema);

// Define the GET endpoint to retrieve all providers
app.get('/providers', async (req, res) => {
  try {
    const providers = await Provider.find(); // Retrieve all providers from the database
    res.json(providers); // Send the provider data as JSON
  } catch (err) {
    res.status(500).json({ message: "Error retrieving providers" });
  }
});

// Start the server on port 3000
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});


QUESTION THREE

const express = require('express');
const mongoose = require('mongoose');

// Create an Express app
const app = express();

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/hospital', { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log("Connected to MongoDB"))
  .catch((err) => console.log("Failed to connect to MongoDB", err));

// Define the Patient schema
const patientSchema = new mongoose.Schema({
  patient_id: { type: Number, required: true },
  first_name: { type: String, required: true },
  last_name: { type: String, required: true },
  date_of_birth: { type: Date, required: true }
});

// Create the Patient model
const Patient = mongoose.model('Patient', patientSchema);

// Define the GET endpoint to retrieve all patients by first name
app.get('/patients/:first_name', async (req, res) => {
  try {
    const firstName = req.params.first_name;  // Capture the first name from the URL
    const patients = await Patient.find({ first_name: firstName });  // Find patients with the matching first name

    if (patients.length === 0) {
      return res.status(404).json({ message: "No patients found with that first name." });
    }

    res.json(patients);  // Return the list of patients
  } catch (err) {
    res.status(500).json({ message: "Error retrieving patients" });
  }
});

// Start the server on port 3000
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});



QUESTION 4

const express = require('express');
const mongoose = require('mongoose');

// Create an Express app
const app = express();

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/healthcare', { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log("Connected to MongoDB"))
  .catch((err) => console.log("Failed to connect to MongoDB", err));

// Define the Provider schema
const providerSchema = new mongoose.Schema({
  first_name: { type: String, required: true },
  last_name: { type: String, required: true },
  provider_specialty: { type: String, required: true },
});

// Create the Provider model
const Provider = mongoose.model('Provider', providerSchema);

// Define the GET endpoint to retrieve all providers by specialty
app.get('/providers/specialty/:specialty', async (req, res) => {
  try {
    const specialty = req.params.specialty;  // Capture the specialty from the URL
    const providers = await Provider.find({ provider_specialty: specialty });  // Find providers with the matching specialty

    if (providers.length === 0) {
      return res.status(404).json({ message: "No providers found with that specialty." });
    }

    res.json(providers);  // Return the list of providers
  } catch (err) {
    res.status(500).json({ message: "Error retrieving providers" });
  }
});

// Start the server on port 3000
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});

