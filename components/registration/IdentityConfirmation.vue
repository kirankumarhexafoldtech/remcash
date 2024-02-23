<template>
    <div class="identity">
        <h2 class="identity-heading">{{identityContent.hedding}}</h2>
        <p class="identity-description">{{identityContent.description}}</p>
        <div class="identity-section" v-if="currentSection==1">
            <div class="identity-scan-details">
                <p>Scan your ID to submit your personal details for verfication.</p>
                <p>We accept following documents:</p>
            </div>
            <div class="identity-available-ids">
                <p v-for="(n,index) in identityContent.ids" :class="selectedId == n.content ? 'identity-available-ids-active' : ''"
                @click="handleSelectingIdentity(n.content)"
                ><span><i :class="n.img"></i></span> {{n.content}}</p>
            </div>
            <button class="main_auth_button identity-section-button-position" @click="currentSection = 2">Proceed with {{selectedId}}</button>
        </div>
        <div v-if="currentSection == 2" class="identity-selected">
                <p>Please scan the {{ selectedId }}, as demonstrated below, to submit your personal details for verification.</p>
            <img :src="identityContent.img" alt="">
            <p>Please upload/scan {{ identityContent.upload.selected == 1 ? 'front' : 'back' }} side of {{ selectedId }}:</p>
            <div>
                <div>Front side of {{selectedId}}</div>
            </div>
            <div class="identity-selected-buttons-postion">
                <button class="main_auth_button identity-selected-button" ><span><i class="ri-qr-scan-2-line"></i></span>Scan ID<span></span></button>
                <button class="main_auth_button identity-selected-button" @click="handleUploadDoc"><span><i class="ri-file-upload-line" id="uploadDoc"></i></span>Upload ID<span></span></button>
            </div>
            <p class="goback identity-select-different-id" @click="handleSelectDifferentId"><i class="ri-arrow-left-s-fill"></i>Select different ID</p>
        </div>
        <p class="goback identity-go-back" @click="handleGoBack" v-if="currentSection == 1"><i class="ri-arrow-left-s-fill"></i>Go back</p>
        <!-- <div id="camera">
            <button @click="startCamera">Start Camera</button>
            <video ref="video" autoplay>k</video>
        </div> -->
    </div>
</template>

<script setup>
import IdentityCard from "@/assets/svg/example_id.svg";

const identityEmit = defineEmits(['goback']);
const router = useRouter()
const video = ref();

const selectedId = ref("National ID");
const currentSection = ref(1);
const identityConfirmation = ref(false);

const identityContent = reactive({
    hedding:"Identity Confirmation",
    description:`Please provide a copy of your ${selectedId.value}.`,
    img: IdentityCard,
    ids:[
        {
            id:1,
            img:"ri-profile-line",
            content:"National ID"
        },
        {
            id:2,
            img:"ri-pass-valid-line",
            content:"Driving liscence"
        }
    ],
    upload:{
        doc:[],
        selected:1
    }

});
// selecting identity card
function handleSelectingIdentity(data){
    selectedId.value = data;
    identityContent.description = `Please provide a copy of your ${selectedId.value}.`
};
// sekecting different id
function handleSelectDifferentId(){
    console.log("clecked")
    currentSection.value = 1;
};
// uploading the document
function handleUploadDoc(){
 
      const fileInput = document.createElement('input');
      fileInput.type = 'file';
      fileInput.accept = 'image/*';
      fileInput.style.display = 'none';      
      fileInput.addEventListener('change', function(event) {
      const input = event.target;
      const file = input.files[0];

        if (file) {
            console.log(file)
          const reader = new FileReader();

        //   reader.onload = function(e) {
        //     const previewImage = document.getElementById('previewImage');
        //     previewImage.src = e.target.result;
        //     previewImage.style.display = 'block'; // Show the preview image
        //   };
        //   reader.readAsDataURL(file);
        }
      });
      // Trigger a click on the dynamically created file input
      fileInput.click();
}
async function startCamera() {
    try {
        const stream = await navigator.mediaDevices.getUserMedia({ video: true });

        // Access the video element and set its source to the camera stream
        const videoElement = video.value;
        videoElement.srcObject = stream;

        // Handle when the user stops the camera
        stream.getVideoTracks()[0].onended = () => {
            console.log('Camera stopped');
        };
    } catch (error) {
        console.error('Error accessing camera:', error);
    }
};

function handleGoBack(){
    console.log("clicked")
    if(!identityConfirmation.value){
        router.push("/auth/register");
        identityEmit('goback',"register")
    }
}

onBeforeUnmount(()=>{
    handleGoBack();
})

function stopCamera() {
      // Check if the camera stream is available before stopping it
    //   if (cameraStream) {
    //     const videoTrack = this.cameraStream.getVideoTracks()[0];

    //     // Stop the video track to stop the camera
    //     videoTrack.stop();

    //     // Log a message indicating that the camera has been stopped
    //     console.log('Camera stopped');
    //   }
}

</script>