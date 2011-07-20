Chatter Profile "Jailbreak"

Joel Dietz / @fractastical
4.16.11

Functionality:

	(1) Uses Javascript embedded in custom component to override default functionality when clicking Profile Tab 
	(2) Javascript loads Profile page in the same page 
	(3) Variables allows easy insertion and modification of custom content

Benefits to this approach:

	(1) Virtually unnoticible  
	(2) All parts of the profile page work as expected
	(3) Actually uses Profile page instead of attempting to simulate it, preserving changes made by Salseforce and maintaining all elements of the profile page (including to-do list)
	(4) No problems with cross-domain scripting (as you would have with a Visualforce page)
	(5) No iframes (eww!)

Incomplete Aspects:

	(1) Would need to be applied to all Chatter related tabs since the override will only be in place so long as the sidebar is in place
	(2) Bug currently prevents contact information modification (all other behavior works as expected). 

How to use:

	(1) Go To Setup -> Customize -> Home -> Home Page Components
	(2) Create new Custom Component of type HTML Area (narrow_
	(3) Edit your custom component. 
	(4) Click "Show HTML"
	(5) Paste the following Javascript into the area (without comments):

	---
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.5.2/jquery.min.js"></script>
	<script>

			//Javascript variables contain content that will be inserted in various places
			var extraContactHTML = 'Made by @fractastical';
			var extraAboutMeHTML = 'I ::heart:: contests';
	        var extraToDoListItemHTML ='<div class="itemBox"><li id="listItem-getChatterMobile" class="incompleteClass"><a href="http://fractastical.com" target="_blank">Visit Fractastical.com</a></li></div>';

			//Hides the HTML sidebar so that it is not visible
 			$('.sidebarModule.htmlAreaComponentModule').hide();  

	        $('#UserProfile_Tab a').click(function(ev) {        
	               ev.preventDefault();             
	               $('#bodyCell').html('').load('/_ui/core/userprofile/UserProfilePage #bodyTable', function(response, status, xhr) { 
	                		if (status == "error") { 
                      				var msg = "Sorry but there was an error loading the profile page: ";
                    				$("#error").html(msg + xhr.status + " " + xhr.statusText);
		                     }  
							else {
									//Adds content from variables specified above
									
									$('.address.profileSectionData').append(extraContactHTML);  
									$('.aboutMe').append(extraAboutMeHTML);  
									$('#mainOuterList.listClass').append(extraToDoListItemHTML);    
							}
							          
					});      
			});    

	</script> 
	---

        (6) If desired, modify HTML in provided variables or add your own
	(7) Navigate to Setup -> Customize -> Home -> Home Page Layouts 
	(8) Add the custom component to your default home page layout
	(9) If desired, add sidebar to all pages via Setup -> Customize -> User Interface -> Show Custom Sidebar Components on All Pages

Now whenever someone clicks on the profile, it will load the modified profile.  


This technique has been tested in Firefox 3.6 and Chrome 11 Beta and appears to be bug free. 


If desired, you can also see active code by logging into this account:

user: jd@fractastical.com
password: fooBirdy1

A Flash/SWF presentation is also included. 

Enjoy!
