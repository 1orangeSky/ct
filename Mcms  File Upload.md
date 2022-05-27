# code analysis
From Mingfei official website https://gitee.com/mingSoft/MCMS

Found upload point after audit，form.ftl  Here is an article thumbnail upload point to see if he has done filtering and then according to  action find upload interface

<img width="815" alt="1" src="https://user-images.githubusercontent.com/106334576/170743233-32ff01e4-ace9-4f32-a21d-6c4e5f23df87.png">
After searching in FileAction.class Only judgment here ../ Prevent directory jumps,Continue to look down and click on the inherited class

<img width="816" alt="2" src="https://user-images.githubusercontent.com/106334576/170743893-34e30e3e-b92c-4c9a-8780-862483bce1e9.png">

BaseFileAction.class I found that he made a suffix judgment and then looked at where the filter was called.

<img width="815" alt="3" src="https://user-images.githubusercontent.com/106334576/170760356-ccc8d566-2336-4f14-9a6f-24a02e7840f0.png">

copy denied Global search,application.yml I found that he wrote the filter in the configuration file filtered exe,jsp,jspx,sh
That means that except for these four others can be uploaded.

<img width="816" alt="4" src="https://user-images.githubusercontent.com/106334576/170760824-20203a6f-bffc-4225-b18a-3650302220e9.png">
<img width="816" alt="5" src="https://user-images.githubusercontent.com/106334576/170761125-af441089-3437-46ca-8605-b49b9a59cac8.png">

See if he has an available interface to upload jsp,searched for TemplateAction.class There is a special analysis zip Interface
Then combined with the above filtering, you can upload zip,able to pass zip Include jsp The malicious file is uploaded and then this interface is called to parse zip
and parse jsp and visit.

<img width="815" alt="6" src="https://user-images.githubusercontent.com/106334576/170762509-410152c6-3331-47c2-8b75-1ea83b756c8b.png">

# Actions based on analyzed code
Find the article thumbnail address and click upload zip
<img width="765" alt="7" src="https://user-images.githubusercontent.com/106334576/170762719-31c2fb2c-e08f-47db-a77a-60554ef0cbcf.png">

<img width="715" alt="8" src="https://user-images.githubusercontent.com/106334576/170763257-ca0ea4c4-682a-4468-b48b-56f149fedb4a.png">

After uploading, right-click to copy the image path, and then parse through the call analyzed above zip Interface fileUrl=  just uploaded zip
Enter to prompt successful execution 

<img width="715" alt="9" src="https://user-images.githubusercontent.com/106334576/170763778-7b9d1d76-c7b4-4a11-873d-52615740fed6.png">

<img width="716" alt="10" src="https://user-images.githubusercontent.com/106334576/170763807-499faaa6-3506-4cee-a152-de712e366473.png">

<img width="716" alt="11" src="https://user-images.githubusercontent.com/106334576/170763831-d4e5f003-9951-43a1-92bd-3a45c8f6eda0.png">

After looking at the upload directory, I found that the decompression was successful and we were accessing it through the path aaaaa.jsp
Then use Godzilla to connect to him and find that the execution is successful

<img width="716" alt="12" src="https://user-images.githubusercontent.com/106334576/170764087-f19fec7f-b0b1-4187-bc43-2072977592b4.png">

<img width="715" alt="13" src="https://user-images.githubusercontent.com/106334576/170764112-7b7f32ab-4cdc-474b-aa09-0517908fa155.png">

<img width="715" alt="14" src="https://user-images.githubusercontent.com/106334576/170764154-fb4e6df6-efdb-472b-95dd-e3feec970654.png">
