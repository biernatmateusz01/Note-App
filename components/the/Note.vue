<template>
  <div
    class="relative p-4 shadow-md bg-white rounded-md border-l-8 border-gray-300 overflow-hidden"
  >
    <div
      v-if="note.done === true"
      class="absolute top-0 left-0 bg-black bg-opacity-40 h-full w-full flex items-center justify-center"
    >
      <img
        src="https://cdn2.iconfinder.com/data/icons/greenline/512/check-512.png"
        class="h-16 w-16"
        alt=""
      />
    </div>
    <div class="w-full flex justify-between mb-2 overflow-auto">
      <div class="flex flex-col">
        <span class="text-xs">Dodano:</span>
        <span
          v-if="note.hasOwnProperty('creationDate')"
          class="text-yellow-400 text-sm font-semibold"
          >{{ note.creationDate }}</span
        >
      </div>
      <div v-if="!note.done" class="flex gap-1">
        <button @click="$emit('delete-item', $event)">
          <img
            src="https://www.svgrepo.com/show/21045/delete-button.svg"
            class="h-4 w-4"
            alt=""
          />
        </button>
        <button @click="$emit('edit-item', $event)">
          <img
            src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAb1BMVEX///8AAAD09PTY2NjU1NTu7u5tbW1ZWVnx8fEnJyf19fVsbGwpKSk3NzcjIyNcXFwaGhoVFRUwMDC7u7uMjIykpKSVlZXIyMhFRUVPT0/j4+NKSkre3t5iYmIRERHHx8d7e3t/f388PDytra2ZmZkWJ9VpAAAEvElEQVR4nO2c6XbiMAyFk7CFUAoFAmUrUHj/ZxwI2MhrcjIMsTL3+9c47dFFkiUvNIoAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAlrLJF/3t/rQ8JE1b8k/Ilr+xZLRq2pzXk09jhcGuaYteS/YdG+RNG/VKdl+mwDg+Nm3W6+ja9F2ZNG3Yq+g4BLZGolvgdb5p2rhXoIbodr+ftUwiFfiTp9cn2e7YpkClIbrOxNNVeyRSgXvHc9aB2nUIVEcYS6Se6nvG9tbfZoBSJgwVLQhUrZMxVLhDmAlGq2ZMmtSLyyZM/DssnYw3UOdNGPk3WFs1I1DJW8PM9mfCxbGa8OUir+UiFdj31gUy2IShddHqIP3RmG6eH8ahCVPr0VUFljQwuRg5vd/SmhgC1UeGF+Vq6t2G1oXG5Mj2UM/FBTOFjl7U06PJpRSPfWIajyPXwMD+Kyx2UC05KHAGqvRh752W1sSag7ZBOt3IyfSNhtbFtx6MnLm45aPQmYO2F6TEg+czCYwSD+qvPHIxlRv+wa8uKgi05GL23D0NfXHhmUVdr10DNXmeKYbetFUUqO1d9MihW+C1wlsm3K8SLu8xtC6eHEyNGcQqseRjaRpPmUim5iRp2QAYv83WWnhyMCtO70u9+BF2EnpCNHlcTyiROEzfZmwdfDnorOYdejNjGPayyZODGbmfoN2fScckRPl4UBdI/LRVh1JyDjzkm4PEg2tt6JNliOo5SDyobVv0iAc/2QrMftwCaQ7yCVFPDn6rQ8kH8SAfgXqIuj2Y8sxBS6tWIUQDL/SlrdodbRZNeeago1WzCFTKBFsP+soEnWT45OD/XCa0Vi2hhZ6PQE+Z0CeZ1peJdrRq7ma7/TlIZ9Gwy0SlFb0ZosNW5KBHIM8Vfb1Wje+KvldxRR+2B3tugdHcHaJ8ykR0dAskp/F8W7Uoe874R8vwQ6K+oufTqilZeLSNryweVFq10I9Ao4snDQtWnFf0NyZxmcSDFqKccvBKFselElUS2smE78HnrZCqEumKPvBW7c5CU1h2bMuoVXvwqSv0e5HR4cuD1BDolcioVRPItmzxU0Gi0qoFXwfv9IXBaYWrM8zKxB0RdeMK97sYHb48kaouUen9IEa7agR5zbU4kPcGKrNWTSBbtvuPvl19jjlIdpnE9WVnLjIsEwXSZ7nxRJXI6PBFRbZsG/nIuu3Gr1UTiHugM/LMEqisVvQKiTD7SJ8aEnmWiQLZsqn307Rc5LSrpiN32Tbqc0Uiy1ZNIAz/1gccV5p55eCVnbB8YQxZJTLLwStnYbrlf5B1fwyBvMpEgdayqSwND3IL0SjKRBFY6yOd3PwvZZxaNYHZst3YnPuGuphfmSiQcSi/5Nk7HH9t8hiWiYKBmobdpUNdzLBMFMhdttPtv1cOnOpuHuQYovQrkKehT971BSa7ajrGZreN9bK7YhmhN6Zl6qan4L/+6aXnVfexP2/K/0bYnN3yJpcO08xTGNnVzRYrnhOnydhU99WfM2zNnKy1aWWSd5o26cWQu0DxetFtk/ME+4e847wtiWcwH8wm/GsCAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAaBN/AIRiK/yTIZQQAAAAAElFTkSuQmCC"
            alt=""
            class="w-6 h-6"
          />
        </button>
        <button @click="$emit('mark-done', $event)">
          <img
            src="
        data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAflBMVEX///8AAAB7e3vNzc14eHj8/Pzz8/NFRUXm5ubPz8/w8PA1NTXDw8PZ2dktLS3U1NSurq5DQ0OhoaGSkpKnp6dQUFC1tbWFhYXIyMhWVlZxcXG5ubmqqqoJCQng4OAfHx9jY2OLi4sRERE8PDyampokJCQoKChpaWkXFxdTU1Nt6iRLAAAMMUlEQVR4nNVd12LqMAwllFD2KKtAgTBauP//g7cppZAjOfG2OY+l2BaytSxLtZprpM1+bzRZ1M+z7mB32SSbw2XXnWWNxWne2zZT5/O7RNpfT7JBUo5uNpn3Q69UB9t5o4q2Rxwb823oJStgO80UiLtjOW2FXroE0t7qoEXeFbtVL+qT2RktDaj7Y+WoE5oQHunaBnlXzObxcXK4skbeFedhaJIekX6oyE1ZfE1jYeS27oC8K+oxCNehvdPHIQttDQxfndKX47Udkr6Zc/p+aAwldPpu9+cj/oUw6ZrK6uGw+xx0x6/j47ePoUzjwrtcfZNf3LI+XQ9bnWbxB+q03ufT+nIjPczIK30vckw41qfDqt8+7Y8WY6nRBv7EaiqzQZdvffmN1WyfZIRy3SFRj+hVrqS7f9EY931fbRm9W6eGIj1XLOI41XcNWtNuxegr5xLnvYJ7b6Z21nZyKZ1h49gAWJTOvrCjtl7Kt8nEyiQ8OmV7aPdhbwM1p2XCetysHkEPZSJm3LM82fuxZDYdQSaBiXjGmQvL8aVETb45mK8mtkKXrlRxW6wkz9Yn63yJ5ho42jI/6AnP49iy2uiLJjqs7U5EMBJZrhur/r9QC+5tziKAUENZ1IwjwRQzP2GUrUisWts/Ik/Jnz8zdbsCgZaY+YxMdwRS1YrW2PNjT22MrYCTMxJ5Ar/8B076vEV+Mh2X36K+XNEieIPckIu8kJnbWbEyPtjVGIkbdshNuNta3vAwMPpZZ8Kd7yKBDhvo0Lb7h9xomb3laoF1ADQtjw431sLuejXABfo2WmZ4+skMZSybLWDPHR2dgf4xA33YXq0WOAG/Uh+G+6VCaQkER6KyWuTEqO1QjD44LaboS3FSJhYO5uCcDTUtxoQNYyKQ3aivKt9ncg98+xJVYAxmhVAxcwhdBpr10KCLlLZtmvS79oN35qDWzUX2qzSzUGmLewO1USW9ujn54iGW5KQiGIEvpTKYPRpDZhIH6hpsZL5GPWnXQV99UM0v4Rm86HwpGKjIqHbPSbyn62Gh+iAJyZXLpYo01kN4BY1rVNheVDz5TdRRB42jlgt+ImaWnhaqD3KpUXpbRHkeMuwkhxZZc9l1A8mmjFdR3EH2aYm/336+PZqDuHpijUG2dKQPHwDkbGWi/yQ3vfG5TDxIgFHEROS2tDMSGsSUzvj/I/ZaPJGnKpCYBs9EFKRxm2tFoPHGeuzkvIZ8BaCKNS6ek5F4XJ9DU9yAMoQxbMhpfaY3nUzwjP4LWgb//K/SCMhE6jHgTVNUj+MkgMqcyEkMecQZXSsD5mpiwiTGV30kxdsFnsQGfA4ffwZZJGL4NpnK565iombxU/wBYrilWF9DRgNZvYz3UUWTDGNWEYSA70mXkj836rus7EPcwwHweP0l6YejzfIYn8BAfuinqXi/J7elUB88/jCwScPb3HCBKRnwg6ua7P5JCsQ7yfVXAd7QSmZaoF12Zz1K0tDBC3IFfZT7Hobd7tIUjqhW+o1F0Ntd2RVBoOkuMOGuIrAyZJIIZPNZwdff3f6OzA17U8FVaJB9tCKiBG7hwkpSJgFBYUUgTW8yGHRF0BgiW2NDflPti1/Mfv8M44X0DDkOqvg5EC/8vfTGzetm7VJgOajkyLHcB5Mtc7BySZhysEZyRq+GG/xw4Qwacw4Ss+aagwBqMpjVbYGD5PrsGoyBMUO5hjY4SP3A/G8Q6w5lstkhkEQV86gvBMR9vJlkYGWL5oBfKje+Ib8kTKIsy0GtB8YQrckfF4BFE0TQWOMgcfTzSygw5ewuXQ72OEhETZf49yHufS1ysIaqYZMizZm9hcvCJgdr5KK3icrCfyIiy0GDKgYQsNhijMa7f29LD/7hhEPBW3vfSVCWt2iNOBJzVIeelYXtLVojF4lvWJPBb4zGPgdrtW1xtD1O4jUX0QEHSYpsHU0an54Fy0HjHBdQfyu4HN5Vj2ANLActJPEUB5yB0fZlPoEsXJzBHxTj20fIwVCOlQ4bu+Sw0liYKw5iVskAbr9VUzBup3imen6dcRBdiU/IeZupDfbgUKsJYTdChiwqyV2JYhkmNQofM/sPKldyTtTEDUXZuSGSRwFF3bqRJ9ElB4lzATxUOof74lDSXHTKwVqtWI5oA+dQKdKGlY0kueiWgxj/PYD2UNIW5A2nFImOOUglTVFbDFSGonUlJDaqQzXxi+IPvwOKlaw2rsJSFYnuFP0fijzrguQ5qAxFXxxVctE9B2tE/5n4Fux6y0h0LWRykNAabBu1VBqurn6JuPHBQfQPG4Y+Pts6QESiDw6Ss7PA0JTqhFy1PwEXvXCQXOWfMDSlHGuTJtEPB5lYm3G8lK3ZSEn0xEGSF9XDmLdGvUApLnojEEVnH0WPzlsgCS762qI15t4C7p6kCksgKrnoj4NcWoKN+8MKLnrkIHIsdyWs3AGXctEnB/EOOKsR+1mzhkIJF31ykCRa5mmIoD90LxCFJHrlIJku1++gLrSfdAlI9MtBPsMLZte+ueBI3HnmIJsThVlE+jeIsh3KXBbih7y2a9wJjACDe245Ep2+oAab7WqiwT13ZjC+DIkuOUiKuF0zvODS1ChnqJpEx2/gYbYW+1ejPO8qEt1yEI/hzQYFzppV0i1vGOi6isG+OF32+2dI55N8ZCRCGRcdc5DohVtVYDyIhvkYYhKd16EQvv6BRiemeVEiEp1zEHXFPfoLGtE4EZon0T2B4rdr1t8fciR6IFD8/hCNOfMnF5REHyUMsBDPg4kN+sLC6zUk0UuNBghXPMacHLzlLpLohUCsIfTozOM2tdGD5JFEP1U20FMrpIdg1WEb6W1368aDkKnRF+lZ4VOss2SlRcDvwV96ehqOBWmLFxRIv6X8tpe309rb03fsfQf7EGtK+NlYNoFKHasUYE0JxfSvCID6iegD5PGz1YlCFlGdjvVrnqtcG/VLaWQbZc2T1WsjFQOZ/8FGipnnNZoBWcg9oyTZMc90EkndTlZHYa2oZyrZhhX3+G4VZCs/T/1S0s5BIERwL/t8mmAGLF8qUgSkmUIMHbpksMeFC70/EusMXU5JDkRGiut2kpP4HGqfMKZElZN2Ec9Qk510Ky5r+0MzRuOvq0/bOZSeLXJlm/lZpgFILnZ5JgJtoxNXMzIK2lG7IgJDW7bF3aME71wkWIJ+YgRFFMtAGm1W35zRHkox9wqiTUklnD76XiBe+5S2F5NhB3GF4z2K9BDKvaagvQEvERTdZcD0T5O8g6WbO05XkbRUkb6NYPapRjNa56AdyeRf/JB2LDE2ZNnTRSpcmWFUKgle1JSA9upSc2eZXrJx6QymXa5amJ7rBxwTidQaVXaD4u7pzK1OOVmH2efRkEi6yiRaN560GW0sLj+3RbXq5NNmtHF0Q+R2l55JwhhFMehFRpNpm5W0G2IS3rqhlkxiEPXkRFYyDmmGN6ktmhil/3Bt6JNLOGeK3VVmIp5pQ286pAFog+MchgKeqyoQKrBBvbocxgYzT2LX/07dkhjZDyzcHu3Zgb3HUfkdaud6jOdisvQZ8O/QKiN2tugVnBGRw58Nx9lpVjeSaAJPOXlbVgkmVmU6E9a4woMRl7IP/HJYrdPJq9pvHFxvVYGE+Z7Zsjhvcp7GD44u34m8k3uJv2ntG4+cv3jF0lWCWFv8/MZJ37S9cLrk7KJ0bQl9rvxU1tX4xattW7WHPSkf4awWcIcJMv7h8mbPBGhOsV3jI5Yu/TfOwb7jbCfZr30uncVxE5WynfqNwclUhrdOZexLko3zatVNsUy9onvSF62tadk5yGHjrUsluGhlEZ8LnVT/9r6KvOTgqVd4yruiRSxPL/KSJ+1P2QgTwKPj3S4/KzcMGtNhldxL+6NFmWK4Y+w381zkUTF4PU/m761OkaNpszNcT+vLTfX3f+E93t4pF+kMDrvPQXf8Oj52BztMea3EPkQMs1/+9N4mGqESXV9kq5mYIQuZ7dJ2z8cs9NOWvvJ5VMI5hmyl1t4ZfYsY6PvBqNIa0UD3I6pUrKGMnaOCevje4ATrKptcHudYMgYQnbkNIrN5VLsTkfZWyvbKAz5XvajJ+8VWylEgOKxG0YhOCWznDWGElcFrY/5M1N2Q9teTrIrO7urUC221GCJt9nujyaLxb3C5HL6dpc3hsuvOssbiNO9tm+5P3X/9foxodXE45gAAAABJRU5ErkJggg==
          "
            alt=""
            class="w-4 h-4"
          />
        </button>
      </div>
    </div>
    <div class="flex justify-between gap-4">
      <p class="text-lg font-semibold text-gray-700">{{ note.title }}</p>
    </div>
    <span class="mt-3 text-md">{{ note.text }} </span>
  </div>
</template>

<script setup>
defineProps({
  note: Object,
});

const done = ref(false);

const asDone = () => {
  done.value = !done.value;
};
</script>
