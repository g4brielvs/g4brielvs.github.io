---
layout: post
title: "Getting Started with Dask and Kubernetes"
categories:
    - kubernetes
    - dask
crosspost_to_medium: false
---

<blockquote>
	Dask enables parallel and out-of-core computation. We couple blocked algorithms with dynamic and memory aware task scheduling to achieve a parallel and out-of-core NumPy clone. We show how this extends the effective scale of modern hardware to larger datasets and discuss how these ideas can be more broadly applied to other parallel collections.
<br><b>― Matthew Rocklin </b>
</blockquote>

If you never heard of [Dask](https://docs.dask.org/), it is parallel programming library for Python. The [project](https://conference.scipy.org/proceedings/scipy2015/pdfs/matthew_rocklin.pdf) was presented at SciPy 2015 by [Matthew Rocklin](https://matthewrocklin.com) ans is sponsored by [NumFOCUS](https://numfocus.org).

Dask is built on top of [NumPy](https://numpy.org) and [Pandas](https://pandas.pydata.org) and extends their familiar interfaces to larger-than-memory and parallel computing environments. Moreover, it has a promising future, as Pandas, Jupyter and scikit-learn maintainers also maintain Dask.

Dask also enables distributed computing in pure Python as [opposed to Apache Spark](https://docs.dask.org/en/latest/spark.html#comparison-to-spark).

This guide uses following tools,

- [AWS](https://aws.amazon.com/)
- [aws-cli](https://aws.amazon.com/cli/)
- [Kubernetes](https://kubernetes.io/)
- [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/)
- [kops - Kubernetes Operations](https://kops.sigs.k8s.io/)
- [helm](https://helm.sh) 
- [Dask](https://dask.org/)

# Kubernetes

First, we install `kubectl` and `kops` using [Homebrew](https://brew.sh) or equivalent,

{% highlight shell %}
brew install kubectl kops
{% endhighlight %}

Second, we give `kops` a bucket to store the configurations. 

{% highlight shell %}
aws s3api create-bucket \
    --bucket g4brielvs-kops-state-store
aws s3api put-bucket-versioning \
    --bucket g4brielvs-kops-state-store \
    --versioning-configuration Status=Enabled
aws s3api put-bucket-encryption \
    --bucket g4brielvs-kops-state-store \
    --server-side-encryption-configuration '{"Rules": [{"ApplyServerSideEncryptionByDefault": {"SSEAlgorithm": "AES256"}}]}'
{% endhighlight %}

Then we set the environment variables for `kops` to use,

{% highlight shell %}
export KOPS_CLUSTER_NAME=g4brielvs.k8s.local
export KOPS_STATE_STORE=s3://g4brielvs-kops-state-store
{% endhighlight %}

Now we choose from [EC2 instance types](https://aws.amazon.com/ec2/instance-types/). Note that specially when solving embarassingly parallel problems, we will not require  more often than not expensive machine, rather we may take advantage of more workers.

{% highlight shell %}
kops create cluster \
    --node-count=4 \
    --node-size=t3.micro \
    --zones=us-east-1a
{% endhighlight %}

Now we launch the cluster creation,

{% highlight shell %}
kops update cluster --name ${KOPS_CLUSTER_NAME} --yes
{% endhighlight %}

Now cluster is starting and it should be ready in a few minutes.

{% highlight shell %}
kops validate cluster 
{% endhighlight %}

Once you are done, **REMEMBER** to tear the cluster down. Otherside you will have to pay for the uptime.

{% highlight shell %}
kops delete cluster --name ${KOPS_CLUSTER_NAME} --yes
{% endhighlight %}

# Helm 

Let's get `helm` started,

{% highlight shell %}
brew install kubernetes-helm
helm init
{% endhighlight %}


{% highlight shell %}
kubectl create serviceaccount --namespace kube-system tiller
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'
helm init --service-account tiller --upgrade
{% endhighlight %}

Finally, we install the [Dask Helm Chart](https://github.com/helm/charts/tree/master/stable/dask),

{% highlight shell %}
helm install stable/dask
{% endhighlight %}

After a few minutes, we check the running services,

{% highlight shell %}
kubectl get services
{% endhighlight %}

When launching the Jupyter server, you will be prompted for a password. The default password is `dask`.