---
marp: true
theme: gaia
backgroundColor: #fff
color: #000
---

# AWS Security Alert: Excessive KMS Key Access

## Wiz Issue: "Data asset with sensitive personal data is encrypted by a key that can be accessed by users who have excessive access to key management services."

---

# The Core Problem: Over-privileged IAM Role

*   Wiz has identified the `AWSReservedSSO_AWSAdministratorAccess` role as having `AdministratorAccess`.
*   This grants **unrestricted access** to all resources in the AWS account.
*   This violates the fundamental security **principle of least privilege**.

---

# Why This Is a Critical Risk

*   **Expanded Attack Surface:** Over-provisioned permissions increase the attack surface for potential threats.
*   **Data Breach Potential:** A compromised role with `AdministratorAccess` could lead to unauthorized access or breaches of sensitive, KMS-encrypted data.
*   **Operational Risk:** Accidental misconfigurations or unintended actions due to broad permissions can disrupt services.

---

# Remediation Path: "Fix Unprotected Principal"

*   **Wiz Recommendation:** "Remove Excessive Permissions".
*   **Strategy:** Replace the broad `AdministratorAccess` with a fine-grained, custom policy.
*   **This approach preserves data:** It focuses on *securing access* to the data, not deleting it.

---

# Understanding `AWSReservedSSO_*` Roles

*   **Managed by IAM Identity Center:** `AWSReservedSSO_*` roles are controlled by AWS IAM Identity Center (formerly AWS SSO).
*   **Direct IAM Modification is Not Recommended:** Do **not directly modify** these roles or detach their default policies in the IAM console.
*   **Permissions via Permission Sets:** Manage permissions by creating or modifying **permission sets** within IAM Identity Center.

---

# Key Steps for Remediation - 1. Discovery & Analysis

*   **Analyze Role Usage:**
    *   **Utilize CloudTrail Logs:** Review API calls made by the `AWSReservedSSO_AWSAdministratorAccess` role to identify the specific actions and resources it actually uses.
    *   **Consult Access Analyzer:** Use AWS IAM Access Analyzer to identify unused permissions and refine access.
*   **Identify Minimum Required Permissions:** Determine the precise set of permissions needed for the role's legitimate functions.

---

# Key Steps for Remediation - 2. Policy Creation

*   **Create a Custom IAM Policy:**
    *   Craft a new IAM policy (e.g., "WizReduced-AdministratorAccess") based on the least privilege principle.
    *   This policy should only include the actions, resources, and conditions identified in the analysis phase.
    *   Wiz may provide a starting JSON policy, but it should be carefully reviewed and tailored.

---

## Key Steps for Remediation - 3. Implementation in IAM Identity Center

*   **Access IAM Identity Center:** Navigate to the IAM Identity Center console.
*   **Manage Permission Sets:** Find the permission set associated with the `AWSReservedSSO_AWSAdministratorAccess` role.
*   **Attach Custom Policy:** Attach the newly created "WizReduced-AdministratorAccess" policy to this permission set.
*   **Detach Broad Policies:** Remove the existing `AdministratorAccess` policy from the permission set.

---

# Key Steps for Remediation - 4. Testing & Validation

*   **Crucial Step:** Implement changes first in a **non-production environment**.
*   **Thorough Testing:** Verify that all essential functionalities relying on the role continue to operate correctly with the new permission set.
*   **Phased Rollout:** Consider a gradual deployment to production, possibly starting with a subset of users or accounts.

---

# Important Considerations: Transparency & Buy-in

*   **Collaborative Effort:** This fix requires architectural input and buy-in from all stakeholders (e.g., application owners, security team, operations).
*   **Potential Impact:** Changes to highly privileged roles can have wide-ranging effects.
*   **Documentation:** Clear documentation of the new policy, the rationale for changes, and the testing results is essential.

---

# Important Considerations: Future-Proofing

*   **Continuous Monitoring:** Establish ongoing monitoring (CloudTrail, Access Analyzer) to track role usage and detect permission drift.
*   **Periodic Review:** Regularly review and update permission sets to ensure they align with evolving needs.
*   **Just-in-Time Access:** Explore implementing just-in-time access solutions for elevated privileges when needed.

---

# My Role & Path Forward

*   **Contribution:** Research the issue and remediation paths, focusing on best practices.
*   **Your Expertise is Key:** Implementing these changes requires architectural expertise and understanding of business impact.
*   **Recommendation:** A planned, collaborative approach to implement the **"remove excessive permissions"** remediation via IAM Identity Center permission sets is strongly recommended.
*   **Avoid "Cowboy" Fixes:** Unilateral, unverified changes to critical infrastructure can lead to service disruptions and security gaps.

---

# Next Steps

*   **Discussion:** Discuss this overview and the proposed steps.
*   **Analysis Deep Dive:** Identify who uses this role and what specific permissions they need.
*   **Create the Custom Policy:** Based on our analysis, craft the precise permissions required.
*   **Plan the Rollout:** Define the testing and deployment strategy, prioritizing minimizing risk.
