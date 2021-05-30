# Terraform GKE Example

This repo sets up and manages the GKE instance on our project. It assumes you have gcloud sdk installed, as well as a gcp project set up and ready to use with billing enabled. 

## Steps

#### setting up
First we need to connect our gcloud cli to our gcp project, this can be done via the following line
`gcloud auth application-default login`

#### terraform creation
To apply the terraform state, we simply apply it:
`terraform apply`

This will show everything that will be created / updated / deleted - if it's the first time it's running from nothing, it will be a lot of creates. Creations are notated by a green +, updates by orange ~, and deletions by a red -. You can see the addition of the google container cluster below:
![Cluster Creation plan](./assets/custer-creation.png)


Wait for it to all apply, this could take up to 10 mins. The outputs will look like the following:
![Terraform creating](./assets/terraform-creation.png)


Once this is done we can go over to the console and see we have a GKE instance, with 2 nodes in the correct region. Since we specified a zone, it will create 2 nodes for that zone.
![GCP console showing instances of the nodes](./assets/console-instance-of-gke-2-nodes.png)

#### scaling up example
As an example of what terraform (and infrastructure as code in general) brings, let us try scale that up to having 3 nodes. In oder to do that, we simply change the number of nodes in the `kubernetes.tf` file and apply. This time by using `terraform plan` before we apply, we can view the planned changes. If we're happy with them, we can then apply them and let terraform handle scalling it up.
![GCP console showing instances of the nodes](./assets/terraform-plan-changes.png)

We notice this time that instead of taking 10 mins, it will be drastically quicker, only about 1 minuite, since it doesn't have to recreate evrything that is already there. 


#### clean-up
Now we want to cleanup this project and removing all resources created for terraform. This can also be handled in terraform with 
`terraform destroy`

