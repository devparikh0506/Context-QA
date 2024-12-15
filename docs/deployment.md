# Deployment

Context QA’s backend is deployed on **Google Cloud Run** with **Cloud SQL** and **Redis**. Builds are automated with **Cloud Build** (see `cloudbuild.yaml`).

## GCP prerequisites

- Active GCP account and project
- Billing enabled
- Service account with sufficient rights (e.g. Owner for initial setup), with a JSON key stored securely

## Terraform

Infrastructure is managed via a Terraform submodule. General flow:

1. Clone/init the submodule (see [README](../README.md) and the [submodule guide](https://medium.com/@saverio3107/adding-a-submodule-and-committing-changes-git-terraform-fastapi-6fe9cf7c9ba7)).
2. Copy `terraform.tfvars.example` to `terraform.tfvars` and fill in credentials and project/region/instance names.
3. From the Terraform directory:
   - `terraform init`
   - `terraform apply`

Target specific modules if needed, e.g.:

```bash
terraform apply -target=module.compute_instance
```

## Cloud Build ↔ GitHub

Connect the repo to Cloud Build using the [Connect repository](https://cloud.google.com/build/docs/automating-builds/github/connect-repo-github) steps. Use a GitHub (classic) token with `repo` and `read:user` (and `read:org` if the repo is under an organization).

## Cloud SQL Proxy (local access)

To connect to Cloud SQL from your machine or tools (e.g. DBeaver):

1. **Download the proxy** (example for Linux AMD64):

   ```bash
   curl -o cloud-sql-proxy https://storage.googleapis.com/cloud-sql-connectors/cloud-sql-proxy/v2.8.1/cloud-sql-proxy.linux.amd64
   chmod +x cloud-sql-proxy
   ```

2. **Run the proxy** (replace placeholders with your instance and credentials):

   ```bash
   ./cloud-sql-proxy --credentials-file=/path/to/credentials_file.json 'project:region:instance?port=5432'
   ```

3. Connect your app or client to `localhost` and the proxy port. See [Cloud SQL Proxy docs](https://cloud.google.com/sql/docs/postgres/connect-auth-proxy) for other platforms and options.

## Useful commands

- **Apply only certain modules:**  
  `terraform apply -target=module.<name>`
- **SSH to a GCP VM:**  
  `ssh -i /path/to/key user@EXTERNAL_IP`  
  Ensure key permissions: `chmod 600 ~/.ssh/id_rsa`
- **Test DB connectivity (with proxy):**  
  `psql -h 127.0.0.1 -U your_user -d your_db`

For exact resource names and regions, check the Terraform module definitions and `terraform.tfvars`.
