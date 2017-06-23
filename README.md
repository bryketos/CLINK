# CLINK
Reproducible Cloud-based GWAS QC and Analaysis

Copyright Brian S. Cole, PhD 2017
See LICENSE in this repository for MIT license details.
This is free software BUT AWS RESOURCE UTILIZATION WILL BE BILLED TO YOUR ACCOUNT.

##Requirements

1. An AWS account
2. A GWAS datset in Plink binary format (BED, BIM, and FAM files) e.g. exported from GenomeStudio
3. A web browser - any decent netbook, PC, tablet, or even cell phone should work
4. (Recommended) A PC to upload your data using SSH (You can also transfer by other means incl. S3 or an SFTP pull from the EC2 instance itself).

##Quickstart

1. Pull or download this repo to your computer.
2. Go to the AWS console.
3. Select CloudFormation to go to the CloudFormation console.
4. Upload the CLINK.json template.
5. Select your desired instance type from the dropdown menu, select a key, select the default VPC and subnet (or an existing VPC and subnet if you have one).
6. Put in your email address.  A private link will be mailed here so DO NOT SHARE THIS LINK.
7. Launch the stack.  All resources are automatically provisioned. You should see "CREATE COMPLETE" in green after about 2 minutes.
8. There is a 90 second delay after the instance launches before it sends the email with the link - this is to boot the Jupyter server and clone in the notebook.
9. Check your span folder for the email.
10. Click the link and you should get straight to the Jupyter menu. Click on the CLINK/ folder and launch the GWAS_QC_and_analysis notebook.
11. Run the first cell, then in the second cell, add the name of your Plink filestem containing your GWAS data. Run this second cell to create the folder for your GWAS study.
12. Open a terminal (or command prompt OR SSH program), then upload your data to the instance using the public IPv4 address of the instance which you can get from the AWS console's EC2 service page.
13. Start walking through the notebook cell-by-cell.
14. When you reach the end of the notebook, the final cell should generate download links for you! Run these SFTP commands to grab the cleaned up study, the images, and the CSV file describing the QC pipeline's results.  Optionally you can download the notebook.
15. IMPORTANT: go to the CloudFormation page and click DELETE STACK. The cloud resources are all securely deleted.

###Pro tips:
1. You can fork this repo on Github or download it and edit the Notebook to change the order of the cells and/or add/subtract steps to suit your desired workflow.
   The point of using version control for both the notebook and the CloudFormation template is flexibility!
2. If you're feeling lucky, you can click "Run all cells" in the Jupyter notebook, but only after uploading your data! Follow the notebook down the page as it runs.  I encourage interactive QC (running cells one-by-one) because you can detect quirks in your dataset (e.g. missing gender encodings) and fix them on the fly.
3. Instances smaller than m4.xlarge didn't have enough memory to run some steps like PCA and merging using the dataset I developed the notebook for, but if you have a smaller dataset you might be able to get away with a smaller EC2 instance.
