# RecursiveGPT
Recursive API calling of GPT4 in order to generate ideas for valuable business softwares to build using the GPT4 API, have GPT4 write code for each one. Then iteratively run the generated code, catch errors, provide them back to GPT4, and have it correct and rewrite  the code until it successfully runs and passes all unit tests.


This is a simple proof of concept of using GPT4 to generate a list of ideas for valuable business software applications for OpenAI's GPT4 API,
then loop through each of the ideas and prompt GPT4 to write the python code to build the software for the idea along with corresponding unit tests.
Next, it will recursively run the code, capture errors, append them to the prompt's message list, and call GPT4 again to fix the errors and rewrite the code
until the code runs properly and passes all unit tests.

The RecursiveGPT() object takes three parameters, "max_retry_attempts_per_idea", "output_code_save_directory", and "max_response_tokens". It will continue to
recursively provide the console error output and have GPT4 address the error and rewrite its code "max_retry_attempts_per_idea" per software, and if a software
succeeds, it will save the code to a local python file with a filename corresponding to the idea name in the "output_code_save_directory" with the description
of the idea at the top of the file as a comment, and then move on to the next one. The "max_response_tokens" determines the maximum response length of your
OpenAI API calls to GPT. Additionally "OPENAI_API_KEY" must be provided as an environmental variable (this is saved to the environmental variable automatically
in the "Run Recursive GPT" cell at the bottom of the page for convenience when using this notebook in Google Colab). This code uses the gpt-4 model, so you must
have access to the gpt-4 API in order to run this code. If you don't have access, change the model attribute of the OpenAI API call function in RecursiveGPT()'s
call_gpt_chat() class function to use the previous ChatGPT model instead to "gpt-3.5-turbo" (this will likely cause a significant reduction in performance)
To start the recursive development process, just initialize an instance of the RecursiveGPT() class with those three parameters, and then call it's 
"run()" class function. For example:

gpt = RecursiveGPT(
            max_retry_attempts_per_idea = 5,
            output_code_save_directory = './',
            max_response_tokens = 2048
            )
gpt.run()

It's far from perfect, and I've been seeing somewhere around ~30-50% of the attempted ideas succeed. However, it's relatively fast and fully automated, so it's
extremely cool that you can just run it and walk away, then come back in a few minutes to a folder with several working python scripts for new GPT4 applications.

This was just a late night idea I had and wanted to try out, but GPT4 actually wrote most of the code for it and other than some basic debugging, I haven't
spent much time going through it yet, so it's definitely still a work in progress with lots of room for improvement. That being said, it's a really cool proof
of concept, so I'm pretty optimistic that with a little effort cleaning the code up and optimizing the prompts, it could probably become a pretty powerful tool.
I am particularly interested in experimenting with improving the prompt engineering for how the model is instructed to build unit tests, as well as updating the
idea generation prompting to start creating more advanced applications by attempting more complex ideas, then having more thorough unit tests to correspond with
the increased complexity. I'm guessing that it'd be capable of making some relatively advanced stuff with good enough prompting and higher max_retry_attempts_per_idea.
Happy coding, and let me know if you come up with any cool upgrades or improvements!
