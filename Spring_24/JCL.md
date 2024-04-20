---
aliases:
  - Simple Batch Systems
---
Job Control Language (JCL) is a scripting language used on mainframes and large computing systems to specify and control batch jobs. It provides a means for users to communicate with the operating system, defining the sequence of operations, input data, and output specifications for each job. JCL plays a crucial role in automating and managing batch processing tasks. Here are the key aspects of JCL:

### Components of JCL:

1. **Job Card:**
   - A JCL job starts with a job card that provides information about the job. It typically includes the job name, account information, and other identification details. The job card begins with "// JOB" and ends with "//."

   ```jcl
   // JOB jobname,account,programmer
   ```

2. **Execution Control Statements:**
   - Execution control statements define how the job should be executed. They specify the type of job, priority, and other parameters. Common execution control statements include:

   ```jcl
   // EXEC PGM=program
   ```

   - This statement specifies the program to be executed. `PGM` stands for program.

   ```jcl
   // PRIORITY=n
   ```

   - This statement sets the priority of the job.

3. **Input and Output Specifications:**
   - JCL includes statements for defining input and output specifications. These statements specify datasets to be used as input and where the output should be directed.

   ```jcl
   // INPUT DD DSN=dataset_name,DISP=SHR
   ```

   - This statement defines an input dataset named `dataset_name` with DISP parameter indicating it is to be shared.

   ```jcl
   // OUTPUT DD DSN=output_dataset,DISP=(NEW,CATLG,DELETE)
   ```

   - This statement defines an output dataset named `output_dataset` with DISP parameter indicating it should be created, cataloged, and deleted after use.

4. **Conditional Processing:**
   - JCL supports conditional processing, allowing users to specify conditions under which certain steps should be executed or skipped. Common conditional statements include:

   ```jcl
   // IF (condition) THEN
   // ELSE
   // ENDIF
   ```

   - These statements allow conditional execution of specific steps based on specified conditions.

5. **Job Control Statements:**
   - Job control statements provide additional control over the execution of the job. Examples include:

   ```jcl
   // NOTIFY=user_id
   ```

   - This statement specifies a user ID to be notified upon job completion.

   ```jcl
   // TIME=(5,0)
   ```

   - This statement sets a time limit for the job to execute. If the job exceeds this time, it may be terminated.

### Example JCL Job:

Here's a simplified example of a JCL job:

```jcl
// JOB JOBNAME=EXAMPLE,ACCOUNTING=123456,PROGRAMMER=USER1
// EXEC PGM=MYPROGRAM
// INPUT DD DSN=INPUT.DATA,DISP=SHR
// OUTPUT DD DSN=OUTPUT.DATA,DISP=(NEW,CATLG,DELETE)
// NOTIFY=USER1
// TIME=(5,0)
// IF (STEP1.RC > 0) THEN
//    // STEP2 EXEC PGM=ANOTHERPROGRAM
// ENDIF
// ENDJOB
```

In this example:

- The job is named "EXAMPLE" with accounting information and a programmer's name.
- It executes a program called "MYPROGRAM" with specified input and output datasets.
- It notifies "USER1" upon job completion.
- It has a time limit of 5 minutes.
- If the return code (`RC`) of the first step (`STEP1`) is greater than 0, it executes a second step (`STEP2`) with a different program.

### Additional Considerations:

- **Return Codes (RC):**
  - Each step in a JCL job produces a return code upon completion. Users can use these return codes to conditionally control the flow of the job.

- **Cataloging Datasets:**
  - The `CATLG` parameter in the `DISP` statement catalogues datasets, making them accessible for future reference.

- **System Commands:**
  - JCL can include system commands that interact with the operating system.

### Historical Context:

JCL has its roots in the early days of mainframe computing, where it was used to control and automate batch processing tasks. While the computing landscape has evolved, JCL remains relevant in legacy systems and industries that rely on mainframes for large-scale data processing.

Understanding JCL is essential for mainframe operators, system programmers, and anyone involved in managing batch processing workflows on mainframe systems. While newer computing environments often use different mechanisms for batch processing, the principles of JCL have influenced subsequent generations of job control and scripting languages.