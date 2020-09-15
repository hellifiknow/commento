### Commento for arm on a Raspberry Pi Kubernetes Cluster

##### [Homepage](https://commento.io) &nbsp;&ndash;&nbsp; [Demo](https://demo.commento.io) &nbsp;&ndash;&nbsp; [Documentation](https://docs.commento.io) &nbsp;&ndash;&nbsp; [Contributing](https://docs.commento.io/contributing/) &nbsp;&ndash;&nbsp; [#commento on Freenode](http://webchat.freenode.net/?channels=%23commento)

Commento is a platform that you can embed in your website to allow your readers to add comments. It's reasonably fast lightweight. Supports markdown, import from Disqus, voting, automated spam detection, moderation tools, sticky comments, thread locking, OAuth login, single sign-on, and email notifications.

###### How is this different from Disqus, Facebook Comments, and the rest?

Most other products in this space do not respect your privacy; showing ads is their primary business model and that nearly always comes at the users' cost. Commento has no ads; you're the customer, not the product. While Commento is [free software](https://www.gnu.org/philosophy/free-sw.en.html), in order to keep the service sustainable, the [hosted cloud version](https://commento.io) is not offered free of cost. Commento is also orders of magnitude lighter than alternatives.

###### Why should I care about my readers' privacy?

For starters, your readers value their privacy. Not caring about them is disrespectful and you will end up alienating your audience; they won't come back. Disqus still isn't GDPR-compliant (according to their <a href="https://help.disqus.com/terms-and-policies/privacy-faq" title="At the time of writing (28 December 2018)" rel="nofollow">privacy policy</a>). Disqus adds megabytes to your page size; what happens when a random third-party script that is injected into your website turns malicious?

#### Installation

Read the [documentation to get started](https://docs.commento.io/installation/).

#### Contributing

If this is your first contribution to Commento, please go through the [contribution guidelines](https://docs.commento.io/contributing/) before you begin. If you have any questions, join [#commento on Freenode](http://webchat.freenode.net/?channels=%23commento).

### Recommendations for installing on a Raspberry Pi Kubernetes Cluster

Take a look at the server-deployment.yaml and modify the COMMENTO_ORIGIN env value to reflect your public endpoint (Example: https://commento.yourblogsite.com) and add the SMTP env variables with the settings needed to enable mailing services for your setup. Please see the commento documentation for the specifics on email setup.

In the db-deployment.yaml it might be a good idea to modify the POSTGRES_USER and POSTGRES_PASSWORD values.

Then you can just do:

`kubectl apply -f server-service.yaml -f db-deployment.yaml -f postgres-data-volume-persistentvolumeclaim.yaml -f server-deployment.yaml`

Don't forget to add this to your server-deployment after you have set up your owner user as shown in the commento documentation.

```- name: COMMENTO_FORBID_NEW_OWNERS
       value: "true"
```
