Difficulty: Moderate
Tech Stack: AWS, Terraform
Question: Imagine you have two environments in AWS: staging and production. Both environments are almost identical, but slight variations exist. How would you structure your directories and files in Terraform to reuse the code and reduce duplication? Can you also describe a situation when you would not use modular code?
Hint: Think about the abstract idea of DRY (Don't Repeat Yourself) principle and how it applies to Infrastructure as Code practices. Consider mentioning separate state files, modules, and parameterization. Additionally, think about scenarios where trying to make code modular can introduce needless complexity.
Answer: To structure Terraform code for reusable and DRY principles across multiple environments like staging and production, I would structure my directories and files in a way that encourages code reuse and simplifies configuration. The code that is common to both environments would be encapsulated as modules. 

Here's an example of a possible directory structure:

```
- main.tf (the entry point file)
- variables.tf (extra variables does apply to original code in 'modules')
- outputs.tf (outputs if needed)
- /staging
   - variables.tf (variables' values)
   - main.tf (calls the modules)
- /prod
   - variables.tf (variables' values)
   - main.tf (calls the modules)
- /modules
   - /app
      - variables.tf
      - main.tf
      - outputs.tf
```

By having a separate subdirectory for each environment, we can maintain slight differences in configuration between staging and production by adjusting the variables in each subdirectory's variables.tf file. All the resuable code is under /modules and we call those from main.tf in each environment (staging and prod). 

There will be separate state files for each environment to avoid one environment's changes affecting another. 

However, making code overly modular can sometimes introduce needless complexity and become a hindrance. If an AWS resource or setup is specifically unique to one environment and is never going to be shared with the other environment, it would be better to have the code for that resource or setup directly in the respective environment's subdirectory instead of making it a module. Trying to make it modular just for the sake of modularity and without a practical reuse scenario can lead to confusing and difficult-to-maintain code. For instance, if there is a unique EC2 instance type required only in the production environment and not in staging, this code should be in the production directory, not inside a reusable module.