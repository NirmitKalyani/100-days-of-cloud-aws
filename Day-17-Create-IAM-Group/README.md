# Day 17 – Create IAM Group (AWS)

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by KodeKloud, this task focuses on organizing user access using **AWS Identity and Access Management (IAM)** groups. IAM groups allow permissions to be managed efficiently by assigning policies to multiple users at once.

The objective was to create an IAM group with the required name and verify that it was successfully created.

---

## Concept
An IAM group is a logical collection of IAM users. Instead of attaching permissions to each user individually, permissions are assigned to a group, and all users within that group automatically inherit those permissions. This approach improves security, scalability, and ease of access management.

---

## Real-World Use Case
IAM groups are commonly used to:
- Manage permissions for teams (DevOps, Developers, Admins)
- Implement role-based access control (RBAC)
- Simplify onboarding and offboarding of users
- Ensure consistent permission enforcement across users

---

## Requirements
- **IAM group name:** `iamgroup_ravi`
- **AWS Service:** IAM (Global service)
- **Final state:** Group successfully created

---

## AWS Services Used
- **AWS Identity and Access Management (IAM)**

---

## Steps Performed
1. Navigated to **Services → IAM**.

   ![Navigate to IAM](screenshots/step-1-open-iam.png)

2. Selected **User groups** from the left navigation panel.

   ![IAM User Groups](screenshots/step-2-user-groups.png)

3. Entered the group name as **`iamgroup_ravi`**.

   ![Enter Group Name](screenshots/step-3-group-name.png)

4. Skipped attaching policies (as none were required for this task).

   ![Skip Policy Attachment](screenshots/step-4-skip-policies.png)

---

## Verification
The following screenshots confirm successful completion of the task:

- **IAM groups list showing `iamgroup_ravi`:**

  ![IAM Group Created](screenshots/verification-group-list.png)

- **IAM group details page confirming group creation:**

  ![IAM Group Details](screenshots/verification-group-details.png)

---

## Outcome
The IAM group **`iamgroup_ravi`** was successfully created and is available for adding users and attaching policies as required.

---

## Learnings
- IAM groups simplify access management for multiple users.
- IAM is a global service and does not depend on AWS regions.
- Policies can be attached later without recreating the group.
- Group-based permissions improve security and scalability.

---

**Status:** Completed
