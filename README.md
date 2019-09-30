# Asp.Net-Mvc
Mvc Code Library
# File Upload In Mvc

 #Controller

       [HttpGet]
       public ActionResult FileUploadExampleDemoInMvc() => View();
       
        [HttpPost]
        [ValidateInput(true)]
        [ValidateAntiForgeryToken]
        public ActionResult FileUploadExampleDemoInMvc(HttpPostedFileBase _httpPostedFileBase)
        {
            if (_httpPostedFileBase != null)
            {
                var extension = Path.GetExtension(_httpPostedFileBase.FileName);
                var path = Path.Combine(Server.MapPath("Path to save File goes here ?") + _httpPostedFileBase.FileName.ToString());
                var FD = new FileInfo(path);
                if (FD.Exists == true)
                       FD.Delete();
                STU_PHOTO.SaveAs(path); 
                ViewBag.Success = true;
                return View(nameof(AdmissionPageGenerater), _newAdmission);
            }

            return RedirectToAction(nameof(ViewName));
        }
        
 #View

        @using (Html.BeginForm("FileUploadExampleDemoInMvc", "FileUploadExampleDemoInMvcController", FormMethod.Post, new { enctype = "multipart/form-data" }))
        {
            @Html.AntiForgeryToken() 
            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
            
             <input type="file" name="FIleName" value="" />
             
             <button type="submit">Upload FIle</button>
            
         }
