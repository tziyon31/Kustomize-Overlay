# 🌍 Kustomize Overlay Managing Environments

This project demonstrates how to manage **multiple Kubernetes environments** (dev, staging, prod, QA) using **Kustomize overlays** — layering configuration differences cleanly on top of shared base manifests.

---

## 📁 Step 1 – Folder Structure

Each environment has its own overlay referencing the shared base.

<br><br>

<p align="center">
  <img width="337" height="341" alt="folder tree" src="https://github.com/user-attachments/assets/25ad1c6e-5c51-4188-9874-0087b3589daf" />
</p>

<br><br>

---

## 🚀 Step 2 – Base Deployment

Here’s the **base deployment** for the API service — this manifest is reused across all environments.

<br><br>

<p align="center">
  <img width="250" height="293" alt="base deployment" src="https://github.com/user-attachments/assets/c5b0a021-cce1-4aed-88d1-9cbdacb1e1bb" />
</p>

<br><br>

---

## 🖼️ Step 3 – Environment Overrides (Production Example)

In **production**, we’ll use a different image and updated configuration.

<br><br>

<p align="center">
  <img width="170" height="145" alt="prod image 1" src="https://github.com/user-attachments/assets/c3c536d7-df4b-4178-aba1-6bddcbd0ae94" />
</p>

<br><br>

<p align="center">
  <img width="187" height="165" alt="prod image 2" src="https://github.com/user-attachments/assets/9c231baa-e112-4c3f-af0f-ea80d5ba321f" />
</p>

---

## ⚙️ Step 4 – Base ConfigMap

Our **base ConfigMap** defines environment variables shared across all layers.

<br><br>

<p align="center">
  <img width="174" height="116" alt="configmap base" src="https://github.com/user-attachments/assets/8854ab22-a8e8-4864-845e-8acfeaad66e3" />
</p>

<br><br>

---

## 🔍 Step 5 – Staging Variables

Let’s check how variable values are modified in the **staging** overlay.

<br><br>

<p align="center">
  <img width="169" height="70" alt="staging variable 1" src="https://github.com/user-attachments/assets/fca0e76f-eb61-44ce-bf74-3c6490e06782" />
</p>

<br><br>

<p align="center">
  <img width="182" height="108" alt="staging variable 2" src="https://github.com/user-attachments/assets/0cb39a30-9aad-4dec-bdf4-4d2c5e10cf45" />
</p>

---

## 📊 Step 6 – Inspecting Pod and Environment Differences

**Check how many pods will run in the prod environment:**

<br><br>

<p align="center">
  <img width="962" height="96" alt="grep prod pods" src="https://github.com/user-attachments/assets/933e1c20-725e-4d1a-a741-5043c3290a8e" />
</p>

---

**Now check how many environment variables exist in the dev deployment.**

Base deployment:

<br><br>

<p align="center">
  <img width="236" height="287" alt="base env vars" src="https://github.com/user-attachments/assets/1260f810-1b89-4350-9bbc-4bda6ec369a1" />
</p>

<br><br>

Patch overlay:

<br><br>

<p align="center">
  <img width="247" height="399" alt="env patch" src="https://github.com/user-attachments/assets/979d143c-8458-4e72-b38e-96ffb1cb34a1" />
</p>

✅ **Result:**  
There are **3 environment variables** in the final `api` deployment because all unique keys from the patch are added on top of the base.

---

## 🧱 Step 7 – Changing the API Image in QA Environment

We’ll modify the API image in **QA** to use `caddy`.

<br><br>

<p align="center">
  <img width="288" height="43" alt="qa caddy image" src="https://github.com/user-attachments/assets/d0533ad8-822d-4261-8e45-ee59ab1f0595" />
</p>

Referencing the official Kubernetes documentation:

<br><br>

<p align="center">
  <img width="327" height="626" alt="kubernetes docs" src="https://github.com/user-attachments/assets/9cbc1d37-4844-483f-a822-f9f417bce864" />
</p>

Now, edit the `kustomization.yaml` in the QA overlay to include a **JSON patch** for the new image:

<br><br>

<p align="center">
  <img width="371" height="305" alt="json patch qa" src="https://github.com/user-attachments/assets/7ab5a1a0-09cc-4fe7-997a-74763ed46b92" />
</p>

Build confirmation:

<br><br>

<p align="center">
  <img width="942" height="82" alt="qa build" src="https://github.com/user-attachments/assets/0dd8eea0-83e4-4ae1-b51f-6d9a08e5c3e7" />
</p>

---

## 🚀 Step 8 – Adding a New Deployment to Staging

We can easily extend the staging overlay with new resources, such as an additional deployment.

<br><br>

<p align="center">
  <img width="908" height="98" alt="staging new deployment" src="https://github.com/user-attachments/assets/7580d083-28a6-43e2-ad6e-efa0e85bdf1d" />
</p>

✅ **Done!**  
Each environment now has its own independent configuration layer while sharing the same base logic — making the setup modular, maintainable, and production-safe.

---

## 🧠 Key Takeaways

- **Overlays** in Kustomize enable environment-specific customization without duplicating YAML files.  
- **Patches** (strategic or JSON) let you overrid
