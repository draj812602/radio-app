<template>
  <div class="container-fluid row">
   
    <div class="form-group col-xs-12 col-sm-12 col-md-8 col-lg-8 col-xl-8" id="first">
      
     <div class="input-group">
          <input type="text"  
          class="form-control" 
          id="youtubeUrl"
          placeholder="Paste link here...">
     <div class="input-group-append">
       <button class="btn btn-primary" 
              type="button"
              @click="validateYouTubeUrl">Add</button>

  </div>
</div>
<hr>
  <iframe id="videoObject" 
      type="text/html" 
      frameborder="0" allowfullscreen></iframe>           
    </div>
    <div class="form-group col-xs-12 col-sm-12 col-md-4 col-lg-4 col-xl-4" id="second">
      <h3 class="form-control">Playlist</h3>
      <hr>
 
     
      <ul class="list-group">
        <li v-for="(anchorTag, k) in anchorTags" :key="k" class="list-group-item">
          <a :href="anchorTag.url"  @click.prevent="playVideo($event)">{{anchorTag.value}}</a>
          <span v-if="anchorTag.url!==''"><i class="fas fa-trash-alt"></i></span>
          </li>
      </ul>
    </div>
    </div>
  
</template>

<script>
export default {
  data() {
           return {
             
            anchorTags:
                [{
                    url: '',
                    value: ''
                 }]

                  }
                
                },
  methods:{
    
     validateYouTubeUrl() {    
    
     var url = document.getElementById('youtubeUrl').value
    
     if (url != undefined || url != '') {        
         var regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|&v=|\?v=)([^#&?]*).*/;
         var match = url.match(regExp);
         console.log(match)
         if (match && match[2].length == 11) {
           
             this.anchorTags.push({ url: url, value: url });
              
           

         } else {
             console.log("hells")
             // Do anything for not being valid
         }
     }

},
  playVideo(event){
   
  //console.log(event.target.href)
  const urlToPlay = event.target.href
  var regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|&v=|\?v=)([^#&?]*).*/;
  var match = urlToPlay.match(regExp);
   document.getElementById('videoObject').setAttribute('src', 'https://www.youtube.com/embed/' + match[2] + '?autoplay=1&enablejsapi=1');
  
  }
  }
}
</script>


<style scoped>

input {
  outline: 0;
  border-width: 0 0 2px;
  border-color: rgb(57, 110, 93)
}

.container-fluid{
  margin-top:20px;
}
hr{
  border: 1px solid black
}
h3{
  text-align: center;
  font-weight: 600;
  text-decoration-line: underline;
  color: white;
  background-color: rgb(45, 68, 68)
}

</style>
