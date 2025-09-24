<script lang="ts" setup>
import type {VbenFormSchema} from '@vben/common-ui';
import {AuthenticationLogin, z} from '@vben/common-ui';

import {computed, h, ref} from 'vue';
import {$t} from '@vben/locales';
import {useAccessStore} from '@vben/stores';

import {Image} from 'ant-design-vue';

import OAuth2Login from '#/plugins/oauth2/views/login.vue';
import {useAuthStore} from '#/store';

defineOptions({name: 'Login'});

const authStore = useAuthStore();
const accessStore = useAccessStore();


const imageSrc = ref('');
const refreshCaptcha = async () => {
  try {
    const captcha = await authStore.captcha();
    imageSrc.value = `data:image/png;base64, ${captcha}`;
  } catch (error) {
    console.error(error);
  }
};
refreshCaptcha();

const formSchema = computed((): VbenFormSchema[] => {
  return [
    {
      component: 'VbenInput',
      componentProps: {
        placeholder: $t('authentication.usernameTip'),
      },
      fieldName: 'username',
      label: $t('authentication.username'),
      rules: z.string().min(5, {message: $t('authentication.usernameTip')}).optional()
    },
    {
      component: 'VbenInputPassword',
      componentProps: {
        placeholder: $t('authentication.password'),
      },
      fieldName: 'password',
      label: $t('authentication.password'),
      rules: z.string().min(6, {message: $t('authentication.passwordTip')}).optional()
    },
    {
      component: 'VbenInput',
      componentProps: {
        placeholder: $t('page.auth.captchaPlaceholder'),
      },
      fieldName: 'captcha',
      label: $t('authentication.password'),
      rules: z.string().length(4, {message: $t('page.auth.captchaRequired')}).optional(),
      formItemClass: 'w-2/3'
    },
    {
      component: 'VbenInput',
      fieldName: 'uuid',
      formItemClass: 'hidden',
      dependencies: {
        trigger: (_, form) => {
          form.setValues({
            uuid: accessStore.captchaUuid,
          });
        },
        triggerFields: ['captchaImg'],
      },
    },
    {
      component: h(Image),
      componentProps: {
        src: imageSrc.value,
        width: 120,
        height: 40,
        preview: false,
        onClick: refreshCaptcha,
      },
      fieldName: 'captchaImg',
      formItemClass: 'ml-auto -mt-[74px]',
    },
  ];
});
</script>

<template>
  <AuthenticationLogin
      :form-schema="formSchema"
      :loading="authStore.loginLoading"
      @submit="authStore.authLogin"
  >
    <template #third-party-login>
      <OAuth2Login/>
    </template>
  </AuthenticationLogin>
</template>
