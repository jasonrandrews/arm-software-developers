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
    showQuestion('Q1','yes');
    showQuestion('Q2','false');

  }
</script>

<form action="javascript:handleIt()">
  <p>Does SIMD Everywhere work to port AVX512 to NEON?</p>
  <input type="radio" id="yes" name="arm_run">
  <label for="yes">Yes</label><br>

  <input type="radio" id="no" name="arm_run" value="no">
  <label for="no">No</label><br>

  <div id="Q1_Correct_Answer" class="info_text correct" hidden><p>That's right! Check the Flags output and look for atomics to be listed.</p></div>
  <div id="Q1_Incorrect_Answer" class="info_text incorrect"  hidden><p>That's incorrect. Try again.</p></div>


 <br>  



 <p>When porting code to Arm Neoverse, SSE intrinsics must be re-written to use NEON intrinsics</p>
  <input type="radio" id="true" name="threads" value="true">
  <label for="true">True</label><br>
  <input type="radio" id="false" name="threads" value="false">
  <label for="false">Flase</label><br>  


  <div id="Q2_Correct_Answer" class="info_text correct" hidden><p>That's right! Some Armv8-A processors such as the Cortex-A72 do not support LSE.</p></div>
  <div id="Q2_Incorrect_Answer" class="info_text incorrect"  hidden><p>That's incorrect. Try again.</p></div>



  <input type="submit" value="Check Answers">
</form>


<br>

[<-- Return to Learning Path](/cloud/lse/#sections)


