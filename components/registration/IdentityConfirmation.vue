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
            <button class="main_auth_button">Proceed with {{selectedId}}</button>
        </div>
        <div v-if="currentSection == 2">
            <div>
                <p>Scan face first as shown below  to submit your 
                    personal details for verification.</p>
            </div>
            <img :src="identityContent.img" alt="">
            <button><span><i class="ri-qr-scan-2-line"></i></span>Scan ID</button>
            <button><span><i class="ri-file-upload-line"></i></span>Upload ID</button>
        </div>
        <!-- <div id="camera">
            <button @click="startCamera">Start Camera</button>
            <video ref="video" autoplay>k</video>
        </div> -->
    </div>
</template>

<script setup lang="ts">
import IdentityCard from "@/assets/svg/example_id.svg";


const video = ref();

const selectedId = ref("National ID");
const currentSection = ref(1);

const identityContent = reactive({
    hedding:"Identity Confirmation",
    description:"Please provide a copy of your National ID.",
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
    ]

});

// selecting identity card
function handleSelectingIdentity(data:string){
    selectedId.value = data;
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