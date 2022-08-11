---
title: "Knowledge Check" 
type: docs
toc_hide: true
hide_summary: true
weight: 5
description: >
    Knowledge Check for the Learning Path  
---


<style>
.info_text {
  margin: 5px;
  color: white;
}
.correct {
  background-color: #5B8200;
}
.incorrect {
  background-color: #CF1F1F;

}
</style>



<script type="text/javascript">      


  function showQuestion(Qnum, correctID) {
    if(document.getElementById(correctID).checked) {
      document.getElementById(Qnum+"_Correct_Answer").removeAttribute("hidden"); 
    }
    else {
      document.getElementById(Qnum+"_Incorrect_Answer").removeAttribute("hidden"); 
    }
  }


  function handleIt() {
    // Hide all info_texts by default to clear them.
    document.querySelectorAll('.info_text').forEach(item => {
      item.setAttribute("hidden","");
    })

    // Use logic per Question to determine correct or incorrect show.    
    showQuestion('Q1','any');
    showQuestion('Q2','false');

  }
</script>

<form action="javascript:handleIt()">
  <p>What is SVE vector length?</p>
  <input type="radio" id="128" name="sve_length">
  <label for="128">128 bits</label><br>

  <input type="radio" id="any" name="sve_length">
  <label for="any">Any vector length from 128 to 2048 bits</label><br>

  <div id="Q1_Correct_Answer" class="info_text correct" hidden><p>That's right!</p></div>
  <div id="Q1_Incorrect_Answer" class="info_text incorrect"  hidden><p>That's incorrect. Try again.</p></div>


 <br>  



 <p>Is SVE supported on all Arm v8-A processors?</p>
  <input type="radio" id="true" name="sve_armv8">
  <label for="true">Yes</label><br>
  <input type="radio" id="false" name="sve_armv8">
  <label for="false">No</label><br>  


  <div id="Q2_Correct_Answer" class="info_text correct" hidden><p>That's right! Not all Arm v8-A processors support SVE instructions. However, they can still run SVE applications using the Arm Instruction Emulator.</p></div>
  <div id="Q2_Incorrect_Answer" class="info_text incorrect"  hidden><p>That's incorrect. Try again.</p></div>



  <input type="submit" value="Check Answers">
</form>


<br>

[<-- Return to Learning Path](/hpc/get_started_mpi/#sections)