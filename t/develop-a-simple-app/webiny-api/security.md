# GraphQL - Security

Webiny API has a built-in entity and API security layer. Based on current identity \(eg. anonymous user, logged in user or even API key\), it lets you manage:

1. **Entity permissions** - create, read, update and delete \(CRUD\) permissions for any [registered entity](creating-a-new-entity.md#register-entities) class
2. **GraphQL access** - define allowed operations and exposed fields

For example, you might want to enable read and update operations on specific entities for one group of users, and only read operation for others. So, you would need to set both entity permissions, and enable GraphQL access.

{% hint style="info" %}
By default, because of the security reasons, no CRUD and GraphQL operations are allowed by default, so it's up to the developer to do the management on his own.

To learn more about the security module, click [here](../../../reference-manual/untitled-1/security-module.md).
{% endhint %}

## Entity permissions

Let's continue with our Library app, and manage security for our three entities.

To manage the CRUD settings, we need to open the security module in Webiny administration, more specifically, the **Entities** section. 

![](../../../.gitbook/assets/image%20%2816%29.png)

The section can be found on the following URL: `{BASE_URL}/admin/security/entities`. Once opened, you should see the list of all registered entities and its permissions.

![Entity permissions.](../../../.gitbook/assets/image%20%283%29.png)

At this point, for all three entities, let's just enable "read" operation under the **Other** column, by clicking the "R" labeled button in "Other" column. Changes are saved automatically as clicked.

![](../../../.gitbook/assets/image%20%2813%29.png)

But we're not done yet. Although this will enable read operation on entities, we still have to enable access for related GraphQL operations.

## GraphQL permissions

In order to manage GraphQL operations access, let's open **Groups** section.

![](../../../.gitbook/assets/image%20%2810%29.png)

Once clicked, you should have the following list of groups:

![](../../../.gitbook/assets/image%20%2815%29.png)

The "Default" is a group that holds all identities and also non-logged-in users. 

![](../../../.gitbook/assets/image%20%2811%29.png)

