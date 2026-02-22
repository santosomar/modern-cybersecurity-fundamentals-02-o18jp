# Access Control Models

Access control is a fundamental component of information security that dictates who is allowed to access and use company data and resources. By effectively managing access to IT resources, organizations can mitigate the risk of data breaches, intellectual property theft, and system compromise.

In this section, we cover the four primary access control models used in modern computing environments.

## 1. Discretionary Access Control (DAC)

Discretionary Access Control (DAC) is an access control model where the owner of an object (like a file or a folder) has full control over who is allowed to access that object and what permissions they have.

### Key Characteristics
*   **Data Ownership:** Every object has an owner. The user who creates a file becomes its owner.
*   **Discretion of the Owner:** The owner can grant or revoke access to any other user or group at their discretion.
*   **Access Control Lists (ACLs):** DAC is typically implemented using ACLs associated with each object, listing users/groups and their permitted operations (Read, Write, Execute).

### Examples
*   The default file permission system in Windows (NTFS permissions) and traditional Linux/UNIX systems (e.g., `chmod` permissions).
*   A user sharing a Google Doc and explicitly giving a colleague "Editor" or "Viewer" access.

### Pros and Cons
*   **Pros:** Highly flexible, user-friendly, and simple to implement for general-purpose computing.
*   **Cons:** Decentralized control means security relies entirely on the users. A compromised user account or a malicious insider can easily exfiltrate or share sensitive data they own, making it unsuitable for highly secure or classified environments.

## 2. Mandatory Access Control (MAC)

Mandatory Access Control (MAC) is the strictest of all access control models. In MAC, access decisions are strictly regulated by the operating system or access control mechanism based on fixed security clearances and data classifications, rather than user discretion.

### Key Characteristics
*   **System Enforced:** The system enforces the access control policy; users cannot override it, even if they own the file.
*   **Labels and Clearances:**
    *   **Objects** (files, databases, systems) are assigned security **labels** or classifications (e.g., Confidential, Secret, Top Secret).
    *   **Subjects** (users, processes) are assigned security **clearances** indicating their authorized level of access.
*   **Lattice-Based Access Control:** Access is heavily dependent on comparing the subject's clearance against the object's classification (e.g., the Bell-LaPadula model for confidentiality: "No Read Up, No Write Down").

### Examples
*   SELinux (Security-Enhanced Linux) and AppArmor in Linux environments.
*   Trusted Solaris or systems used in military and intelligence agencies.

### Pros and Cons
*   **Pros:** Extremely secure, protects against accidental or intentional data leakage by users, immune to many forms of malware that rely on user permissions.
*   **Cons:** Extremely complex to implement and maintain, lacks flexibility, and requires significant administrative overhead to classify all data and manage clearances.

## 3. Role-Based Access Control (RBAC)

Role-Based Access Control (RBAC) is the most widely used model in enterprise environments today. Access is granted based on the user's role within the organization rather than their individual identity.

### Key Characteristics
*   **Role Assignment:** Users are assigned to one or more roles based on their job functions (e.g., "HR Manager," "Database Administrator," "Helpdesk Tier 1").
*   **Permissions Assigned to Roles:** Permissions are associated with the roles, not directly with the users. When a user is assigned a role, they inherit all the permissions given to that role.
*   **Principle of Least Privilege:** RBAC makes it easier to enforce the principle of least privilege, ensuring users only have the access necessary to perform their specific job duties.

### Examples
*   Microsoft Active Directory (AD) using Security Groups.
*   AWS IAM Roles, Kubernetes RBAC (Role and RoleBinding).

### Pros and Cons
*   **Pros:** Highly scalable, simplifies administration (when a user changes jobs, their roles change, and permissions follow automatically), reduces administrative errors, and is easy to audit for compliance.
*   **Cons:** "Role explosion" can occur if roles are not carefully designed, leading to having more roles than users. It lacks context awareness (e.g., it doesn't care *when* or *from where* a user acts).

## 4. Attribute-Based Access Control (ABAC)

Attribute-Based Access Control (ABAC) is the most flexible and advanced access control model. It evaluates a set of attributes—characteristics of the user, the resource, the environment, and the action—against a set of rules (policies) to make a dynamic access decision.

### Key Characteristics
*   **Dynamic and Context-Aware:** ABAC does not rely on static roles. Instead, it computes access decisions in real-time.
*   **Uses Attributes:**
    *   **Subject Attributes:** User's department, clearance level, job title.
    *   **Object Attributes:** Data sensitivity, creation date, project tag.
    *   **Environmental Attributes:** Time of day, IP address, geographical location, device posture (is the laptop patched?).
    *   **Action Attributes:** Read, Write, Delete, Approve.
*   **Policy Engine:** An authorization engine evaluates policies like: *"Allow access to Confidential Data IF the User's Department is Finance AND the Time of Day is between 9 AM - 5 PM AND the Device Posture is Compliant."*

### Examples
*   Next-Generation Firewalls implementing policies based on AD group + Device health + geographic location.
*   Cloud-native zero-trust architectures and advanced IAM policies (e.g., conditional access in Azure AD / Entra ID).
*   XACML (eXtensible Access Control Markup Language) implementations.

### Pros and Cons
*   **Pros:** Extremely granular, highly flexible, supports Zero Trust architectures natively by considering environmental context.
*   **Cons:** Complex to conceptualize, design, and implement. Requires robust metadata tagging for objects and attribute synchronization across identity providers. Performance can be a concern if policy evaluation is too complex.


## References & Further Learning

**HackerRepo (GitHub)**
*   [Cheat Sheets](https://github.com/The-Art-of-Hacking/h4cker/tree/master/cheat-sheets)

**Hacker Training**
*   [Practical Cybersecurity Fundamentals (Video Course)](https://learning.oreilly.com/course/practical-cybersecurity-fundamentals/9780138037550/)
*   [Certified in Cybersecurity - CC (ISC)²](https://learning.oreilly.com/course/certified-in-cybersecurity/9780138230364/)
*   [CCNP and CCIE Security Core SCOR 350-701 Official Cert Guide](https://learning.oreilly.com/library/view/ccnp-and-ccie/9780138221287/)
