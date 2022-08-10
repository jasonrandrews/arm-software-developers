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
    showQuestion('Q1','-g');
    showQuestion('Q2','true');

  }
</script>

<form action="javascript:handleIt()">
  <p>Which compiler option enables debugging symbols?</p>
  <input type="radio" id="-d" name="dbg_option">
  <label for="-d">-d</label><br>

  <input type="radio" id="-g" name="dbg_option">
  <label for="-g">-g</label><br>

  <div id="Q1_Correct_Answer" class="info_text correct" hidden><p>That's right!</p></div>
  <div id="Q1_Incorrect_Answer" class="info_text incorrect"  hidden><p>That's incorrect. Try again.</p></div>


 <br>  



 <p>Which compiler options output vectorization report?</p>
  <input type="radio" id="true" name="vec_report">
  <label for="true">-fopt-info-vec with GNU Compilers and -Rpass=vector with Arm Compiler for Linux</label><br>
  <input type="radio" id="false" name="vec_report">
  <label for="false">-fvectorization with GNU Compilers and -Rvectorization with Arm Compiler for Linux</label><br>  


  <div id="Q2_Correct_Answer" class="info_text correct" hidden><p>That's right!</p></div>
  <div id="Q2_Incorrect_Answer" class="info_text incorrect"  hidden><p>That's incorrect. Try again.</p></div>



  <input type="submit" value="Check Answers">
</form>


<br>

[<-- Return to Learning Path](/hpc/get_started_mpi/#sections)