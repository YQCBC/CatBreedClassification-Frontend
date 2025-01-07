<template>
  <q-page class="q-pa-md">
    <q-file color="teal" filled v-model="fileModel" label="選擇圖片">
      <template v-slot:prepend>
        <q-icon name="cloud_upload" />
      </template>
    </q-file>

    <q-img v-if="fileModel" :src="imgURL(fileModel)" class="fit q-mt-md" />

    <q-btn class="fit q-mt-md" outline rounded label="辨識" @click="fetchBreed" />

    <div>
      <!-- 阿比西尼亞貓 -->
      <div v-if="breedModel === 'Abyssinian'">
        <h2>阿比西尼亞貓 (Abyssinian)</h2>
        <p>特徵：修長的身材、短毛，毛色通常為暖棕色或紅棕色，活力旺盛，喜歡探索。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>牙齒問題：易患牙病，需定期清潔。</li>
          <li>高活動需求：若缺乏運動，可能導致壓力。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：高蛋白低脂的乾糧。</li>
          <li>運動：提供足夠的空間和互動玩具。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>高蛋白低脂乾糧</li>
          <li>互動型逗貓棒</li>
          <li>益智玩具</li>
        </ul>
      </div>

      <!-- 孟加拉貓 -->
      <div v-if="breedModel === 'Bengal'">
        <h2>孟加拉貓 (Bengal)</h2>
        <p>特徵：豹紋或大理石花紋的短毛，外觀野性化，精力充沛。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>腸胃敏感：容易因飲食不當引發腸胃問題。</li>
          <li>高活動需求：缺乏刺激可能導致行為問題。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：容易消化的腸胃保護配方。</li>
          <li>運動：提供爬架和跳躍類玩具。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>腸胃保護配方貓糧</li>
          <li>貓抓板</li>
          <li>爬架</li>
        </ul>
      </div>

      <!-- 緬甸貓 -->
      <div v-if="breedModel === 'Birman'">
        <h2>緬甸貓 (Birman)</h2>
        <p>特徵：長毛，奶油色身體，深色耳朵與四肢，白色手套，溫和黏人。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>心臟病：有患心肌病的風險。</li>
          <li>毛發問題：容易打結，需定期梳毛。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：支持心臟健康的配方。</li>
          <li>毛發護理：每天梳毛以防止打結。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>心臟健康配方貓糧</li>
          <li>梳毛工具</li>
          <li>輕柔毛絨玩具</li>
        </ul>
      </div>

      <!-- 孟買貓 -->
      <div v-if="breedModel === 'Bombay'">
        <h2>孟買貓 (Bombay)</h2>
        <p>特徵：全黑短毛，宛如迷你黑豹，親人、愛互動。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>肥胖：需控制飲食量。</li>
          <li>心理需求：需要互動和關愛以避免壓力。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：低熱量食品以控制體重。</li>
          <li>心理刺激：提供互動型玩具。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>低熱量貓糧</li>
          <li>雷射玩具</li>
          <li>小型追逐球</li>
        </ul>
      </div>

      <!-- 英國短毛貓 -->
      <div v-if="breedModel === 'British_Shorthair'">
        <h2>英國短毛貓 (British Shorthair)</h2>
        <p>特徵：圓臉、厚實被毛、藍灰色最常見。性格溫和、獨立、安靜。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>肥胖：需控制飲食和保持運動。</li>
          <li>牙齒問題：易患牙結石，需定期清潔。</li>
          <li>心臟病：有患肥厚性心肌病的風險。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：高蛋白、低脂貓糧，控制體重。</li>
          <li>運動：提供玩具，鼓勵日常活動。</li>
          <li>毛發護理：定期梳理，特別是在換毛期。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>控制體重的低脂貓糧</li>
          <li>洁牙零食</li>
          <li>貓抓板和玩具</li>
        </ul>
      </div>

      <!-- 埃及貓 -->
      <div v-if="breedModel === 'Egyptian_Mau'">
        <h2>埃及貓 (Egyptian Mau)</h2>
        <p>特徵：中型短毛貓，皮毛帶有自然斑點花紋，性格敏捷忠誠。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>壓力敏感：容易受環境影響。</li>
          <li>高活動需求：需要運動以維持健康。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：高蛋白濕糧。</li>
          <li>環境：提供安靜舒適的居住環境。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>高蛋白濕糧</li>
          <li>跳躍類玩具</li>
          <li>舒壓補充品</li>
        </ul>
      </div>

      <!-- 緬因貓 -->
      <div v-if="breedModel === 'Maine_Coon'">
        <h2>緬因貓 (Maine Coon)</h2>
        <p>特徵：大型長毛貓，尾巴毛茸茸，性格溫柔友善。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>髖關節問題：需定期檢查。</li>
          <li>毛球問題：長毛需頻繁梳理。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：大顆粒飼料以便咀嚼。</li>
          <li>毛發護理：定期梳理毛髮。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>大顆粒飼料</li>
          <li>梳毛工具</li>
          <li>爬架或貓隧道</li>
        </ul>
      </div>

      <!-- 波斯貓 -->
      <div v-if="breedModel === 'Persian'">
        <h2>波斯貓 (Persian)</h2>
        <p>特徵：長毛，扁臉，溫和安靜，喜歡被人陪伴。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>呼吸問題：需保持清潔環境。</li>
          <li>毛發問題：容易打結，需頻繁梳毛。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：毛球控制配方。</li>
          <li>毛發護理：每日梳理毛髮以避免毛球堆積。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>毛球控制貓糧</li>
          <li>梳毛工具</li>
          <li>輕柔毛絨玩具</li>
        </ul>
      </div>

      <!-- 布偶貓 -->
      <div v-if="breedModel === 'Ragdoll'">
        <h2>布偶貓 (Ragdoll)</h2>
        <p>特徵：奶油底色，深色耳朵與尾巴，性格溫順，非常親人。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>泌尿問題：需注意飲水量。</li>
          <li>毛球問題：長毛需定期梳理。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：泌尿保健配方。</li>
          <li>毛發護理：梳理毛髮以防止毛球堆積。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>泌尿保健貓糧</li>
          <li>梳毛工具</li>
          <li>小毛絨玩具</li>
        </ul>
      </div>

      <!-- 俄羅斯藍貓 -->
      <div v-if="breedModel === 'Russian_Blue'">
        <h2>俄羅斯藍貓 (Russian Blue)</h2>
        <p>特徵：短毛銀灰色，翠綠色眼睛，安靜、敏感。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>肥胖：需控制飲食和促進運動。</li>
          <li>壓力敏感：需提供穩定的環境。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：高蛋白低熱量配方。</li>
          <li>環境：提供安靜的空間。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>高蛋白低熱量貓糧</li>
          <li>智能互動玩具</li>
          <li>舒壓補充品</li>
        </ul>
      </div>

      <!-- 暹羅貓 -->
      <div v-if="breedModel === 'Siamese'">
        <h2>暹羅貓 (Siamese)</h2>
        <p>特徵：短毛，奶油身體，深色耳朵與尾巴，愛交談、黏人。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>牙齒問題：易患牙結石。</li>
          <li>心理需求：高度社交性，孤單時可能產生焦慮。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：選用抗牙結石配方飼料，幫助減少牙菌斑。</li>
          <li>互動：提供聲光互動玩具，滿足其高度活躍的性格。</li>
          <li>環境：確保有同伴或足夠的互動時間，避免孤獨。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>抗牙結石配方貓糧</li>
          <li>智能聲光玩具</li>
          <li>舒壓零食</li>
        </ul>
      </div>

      <!-- 無毛貓 -->
      <div v-if="breedModel === 'Sphynx'">
        <h2>Sphynx（無毛貓）</h2>
        <p>特徵：無毛、皮膚呈粉紅色或其他顏色，皺紋明顯，性格外向、喜歡與人互動。</p>
        <h3>健康問題：</h3>
        <ul>
          <li>皮膚乾燥：需使用保濕產品，避免皮膚龜裂。</li>
          <li>怕冷：對低溫敏感，需要保暖措施。</li>
        </ul>
        <h3>飼養建議：</h3>
        <ul>
          <li>飲食：高熱量飼料以維持體溫和能量。</li>
          <li>環境：提供溫暖的休息區（如加熱墊）。</li>
          <li>護理：定期給予皮膚清潔和保濕護理。</li>
        </ul>
        <h3>推薦產品：</h3>
        <ul>
          <li>高熱量貓糧</li>
          <li>保濕護膚品</li>
          <li>暖感毯或加熱墊</li>
        </ul>
      </div>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { api } from 'src/boot/axios'
import { ref } from 'vue'

const fileModel = ref<File | null>(null)

const catData = ref<Record<string, string>>({})

const imgURL = (file: File) => URL.createObjectURL(file)

const breedModel = ref<string>('')

const fetchBreed = async () => {
  const formData = new FormData()
  formData.append('file', fileModel.value as File)

  const response = await api.post('/upload-image/', formData, {
    headers: {
      'Content-Type': 'multipart/form-data',
    },
  })
  breedModel.value = response.data[0].breed
}
</script>

<style scoped>
.text-box {
  white-space: pre-line;
}
</style>
