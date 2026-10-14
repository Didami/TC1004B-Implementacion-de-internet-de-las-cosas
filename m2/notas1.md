# Módulo Software

---

### Cuello de botella - John Von Neumann:

- Procesos paralelos corriendo en "cola".
- Limitación de velocidad en los ordenadores tradicionales donde la CPU (Unidad Central de Procesamiento) y la memoria comparten un único canal de comunicación (bus) para los datos y las instrucciones.

![Arquitectura Von Neumann](./images/arq_von_neumann.png)

---

## Modelo Relacional

### ER diagram

- An ER diagram is a type of flowchart that illustrates how entities relate to each other within a system. They are also called ERDs or ER models.

<img src="./images/ER/1.png" alt="ER diagram symbols" width="600"/>
<img src="./images/ER/2.png" alt="ER diagram example" width="600"/>
<img src="./images/ER/3.png" alt="Company ER diagram exampl" width="600"/>

#### Components:

- Entity: any kind of data object, such as a person, place, or thing.
- Relationship: define how entities act upon each other. They appear as diamonds or as labels on connecting lines.
- Attribute: define the properties of an entity. A descriptive attribute adds detail, and attribute categories include simple, composite, derived, and signle- or multi-value.
- Cardinality: defines the numeric attributes of a relationship. Common types of cardinality in an ER diagram are one-to-one, one-to-many, and many-to-many.
  - <img src="./images/ER/cardinality-symbols-in-chen-notation.png" alt="cardinality chen notation" width="800"/>
  - <img src="./images/ER/cardinality-symbols-in-crows-foot-notation.png" alt="cardinality crows foot notaion" width="800"/>

#### How to create a basic ER diagram:

Start with a plan and build the diagram one layer at a time. Follow these five steps to structure any ERD.

1. Define purpose and scope: Decide what system the diagram covers and why.
2. Identify entities: List the people, objects, and concepts the system tracks.
3. Add relationships: Connect the entities and label how they interact.
4. Add attributes: Attach the properties that describe each entity.
5. Set cardinality: Define the numeric rules for each relationship.

### Primary Key

1. A primary key has to be **unique** and identify only one record in our table.
2. It needs to be **never changing**.
3. A primary key needs to be **never null**.

### Foreign Key

- The same as a primary key, it's just located in a foreign place.

1. Unlike a primary key, a foreign key does not have to be unique. It **can be repeated** inside a table.
2. It's possible to have **multiple foreign keys** in **one entity**.

### Composite Primary Key:

- Are used when two or more attributes are necessary to uniquely identify every record.

1. Use the **fewest** number of attributes as possible.
2. **Don't** use attributes that are apt to change.
