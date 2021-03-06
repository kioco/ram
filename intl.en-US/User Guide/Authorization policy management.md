# Authorization policy management {#concept_glf_vwf_xdb .concept}

Authorization Policy is a collection of permissions defined in Alibaba Cloud. [Elements](reseller.en-US//Policy Language/Elements.md) by a more common deployment. By adding authorization policy for a user or a group, the user or all users in the group can acquire the access permission specified in the authorization policy.

RAM supports two types of authorization policy: [System authorization policy](#) and [Custom authorization policy](#). This paper introduces the management method of Authorization Policy, including: to view the system authorization policy, and create, modify, delete customize authorization policy.

## System authorization policy {#section_01 .section}

System authorization policy is a set of generic authorization policies provided by Alibaba Cloud, specific to the read-only permission or all permissions for different products. For this set of licensing strategies offered by Alibaba Cloud:

-   Users can only be used for authorization, not editing and modification.
-   Alibaba Cloud updates or modifies automatically.

**View system authorization policy**

If you want to view all system authorization policy supported by Alibaba Cloud, log in to The **RAM console**, and enter the **Authorization Policy Management** page, under the **System Authorization Policy** subpage, view or search through the list of system authorization policy.

## Custom authorization policy {#section_02 .section}

If the coarse-grained system authorization policy cannot meet your needs, you can create custom authorization policy. For example, you want to control a specific ECS The operation permission for the instance, or the resource operation request that you request from the visitor must come from the specified IP address, you must use a custom authorization policy to meet this fine-grained requirement.

**Application scenarios**

If you have more fine-grained authorization requirements, such as authorized user Bob can only pair OSSS: /sample\_bucket/Bob/ All objects under perform read-only operations, and limiting IP sources must be part of your corporate network \(through a search engine query, "My IP", you can learn about your corporate network IP Address\), then you can access control by creating a custom authorization policy.

## Create a custom authorization policy {#section_03 .section}

When creating a custom authorization policy, you need to understand the basic structure and syntax of the authorization policy language, please refer to for a detailed description of the relevant content.

**Operation Steps**

After learning about the authorization policy language, you can easily create custom authorization policy to meet the above needs on the **RAM console**.

1.  Log on to the [RAM console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Click**Policy Management** \> **Custom Authorization Policy**.
3.  Click new authorization policy to open the new authorization policy burst window, as shown in the following figure:

    ![](images/3598_en-US.png "New Authorization Policy")

4.  Select a template \(for example, AliyunOSSReadOnlyAccess\). Then, you can edit the policy based on the template, as shown in the figure below:

    ![](images/3599_en-US.png "Edit Authorization Policy")

    The name, remarks, and content of the custom authorization policy have been modified. In the above figure, the selected part is the added fine-grained authorization content.

    The template sample is as follows:

    ```
    
    {
        Version: "1 ",
        "Statement ":[
          {
            "Action ":[
              "Oss: Get *",
              "Oss: list *"
            ],
            "Effect": "allow ",
            "Resource": "ACS: OSS: *: samplebucket/Bob /*",
            "Condition ":{
              "IPaddress ":{
                "ACS: sourceip": "maid"
               }
            }
          }
        ]
    }
    ```

5.  Click new authorization policy to complete the new custom authorization policy.

**Subsequent operation**

If you attach this custom authorization policy to user Bob, then Bob vs. OSS: // samplebucket/Bob/ The object under has read-only operation permissions, and the restriction is that it must be accessed from your corporate network \(assumed to be 121.0.257.1.

Please refer to the specific operation.

## Modify a custom authorization policy {#section_04 .section}

When a user's permissions change \(new permissions are added or existing permissions are revoked\), you must modify the user's authorization policy. When you modify an authorization policy, you may encounter the following problems:

-   Hopefully, after some time, the old authorization policy will continue to be used.
-   After the modification is complete, you find that the authorization policy has been modified incorrectly and needs to be rolled back.

The authorization policy has a version management mechanism that addresses the problems that exist during use:

-   You can retain multiple versions for one authorization policy.
-   If beyond the limit, you need to delete the unnecessary versions.
-   For an authorization policy having multiple versions, only one version is active, which is known as the "default version".

**Operation steps**

1.  Click on the **Policy Management** \> **Custom Authorization Policy**of the **RAM console**.
2.  Through The Authorization Policy Name, which you can use to query by using the keyword, finds the authorization policy that needs to be managed, click the view whose name or corresponding action is listed.
3.  In the left-hand navigation bar, click version management.

     ![](images/3600_en-US.png "Version management") 

4.  As shown in the figure above, on the version management page, you can:
    -   Select to view policy content for all historical versions.
    -   Sets the non-default version policy to the current version \(that is, the default version \).
    -   Select remove non-default version policy.

## Delete a custom authorization policy {#section_05 .section}

You can create multiple authorization policies. Multiple versions can be maintained for each policy. Custom authorization policies no longer needed should be deleted.

**Premise**

Before you delete an authorization policy, you should ensure that:

-   There are no multiple versions of the current authorization policy, and there is only one default version. If multiple versions of the authorization policy exist, you must first delete all versions except the default version.
-   The current authorization policy is not referenced \(that is, attached to a user, user group, or role \). If the Authorization Policy has been referenced, you can:
    -   Unauthorize in the reference record for the authorization policy.
    -   You can also choose to force the relationship to be disassociated during the deletion process.

**Operation steps**

1.  Click on the **Policy Management** \> **Custom Authorization Policy** of the **RAM console**.
2.  The Authorization Policy Name, which you can use to query by using the keyword, finds the authorization policy that needs to be deleted, click the delete on its corresponding action column.
3.  Confirm the deletion of authorization policies, you can choose to check the force disassociate relationship \(when the policy has been referenced records to force a reference relationship to be deleted\).

So far, you have successfully deleted a custom authorization policy.

