# 📊 Sparklyr en mode cluster

## Adapter la configuration

Pour effectuer des traitements avec Sparklyr en mode cluster, il n'y a pas beaucoup de différences avec les traitements en mode local :

<pre class="language-r"><code class="lang-r"><strong>library(sparklyr)
</strong><strong>library(dplyr)
</strong><strong>
</strong><strong># Insérer ici vos configurations personelles pour votre session
</strong><strong>conf &#x3C;- spark_config() 
</strong><strong>conf["spark.driver.memory"] &#x3C;- "16g"
</strong>conf["spark.executor.memory"] &#x3C;- "8g"
conf["spark.executor.core"] &#x3C;- 4
conf["spark.executor.instances"] &#x3C;- 2
conf["spark.yarn.queue"] &#x3C;- "prod"

<strong># Création de la connexion Sparklyr en mode cluster
</strong>sc &#x3C;- spark_connect(master = "yarn", config = conf)
</code></pre>

Notez la présence du paramètre spark.yarn.queue. Il n'existe pas de file par défaut pour forcer le choix vers une des files adaptées. Ne pas préciser ce paramètre amènera le traitement à échouer !

Une fois cette configuration effectuée, il faut effectuer vos traitements comme vous le feriez en mode local.

Attention à l'instruction collect : elle ramène le dataset vers la machine depuis laquelle vous accédez votre session R ! Si le dataset est de taille très importante, cela peut causer une erreur mémoire, car R chargera ce dataset dans la mémoire de la machine et non sur disque. Cette instruction n'est à réserver qu'aux résultats finaux, avec très peu d'unités. Tant qu'il est possible de l'éviter, il faut le faire.&#x20;
