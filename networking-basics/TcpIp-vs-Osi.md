## OSI Model vs TCP/IP Model
The TCP/IP model is almost the same as the OSI model, but the layers are 
grouped differently.

- In **OSI**, Application, Presentation, and Session are three separate 
  layers. In **TCP/IP**, these three are combined into a single 
  **Application Layer**.
- **Transport Layer** remains the same in both models.
- OSI's **Network Layer** corresponds to TCP/IP's **Network Layer / Internet 
  Layer**.
- OSI's **Data Link + Physical Layers** are combined in TCP/IP into the 
  **Network Interface Layer** (also called Network Access Layer).

**TCP/IP model — 4-layer view:**
1. Application Layer
2. Transport Layer
3. Internet Layer
4. Network Interface Layer

**TCP/IP model — 5-layer view** (Network Interface split back out):
1. Application Layer
2. Transport Layer
3. Network Layer
4. Data Link Layer
5. Physical Layer

**In simple words:** The main difference between OSI and TCP/IP isn't the 
functions performed — it's how the layers are grouped together.