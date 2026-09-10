---
aliases:
  - 对话生成器
版本: 1.0.0
icon: BoBxsMessageDetail
cssclasses:
  - chat-noyaml
picfolder: Chat Generator/02 Material/Icon/
charafolder: Chat Generator/02 Material/Character/
notefolder: Chat Generator/01 Chat Notes/
templatePath: Chat Generator/02 Material/Template/Chat Template.md
result2: ""
favid:
charanum:
---

# 对话生成器 Chat Generator

```dataviewjs

let picfolder = '';
let charafolder = '';
let notefolder = '';
let templatePath = '';

const lang = window.moment.locale() && window.moment.locale().startsWith('zh') ? 'zh' : 'en';
const penicon = obsiIcon2('lucide-square-pen', 16);
let personicon = obsiIcon('lucide-user-round', 48);
personicon = personicon.replace(/currentColor/g, '#ffffff');
personicon = personicon.match(/(\<svg)(.*)(?=\<\/span>)/g);
personicon = personicon[0];
let erroricon = obsiIcon('lucide-triangle-alert', 48);
erroricon = erroricon.replace(/currentColor/g, '#ff0066b3');
erroricon = erroricon.replace('"0 0 24 24"', '"-2 -2 28 28"');
erroricon = erroricon.match(/(\<svg)(.*)(?=\<\/span>)/g);
erroricon = erroricon[0];
const replaceicon = '<svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-refresh-ccw-icon lucide-refresh-ccw"><path d="M21 12a9 9 0 0 0-9-9 9.75 9.75 0 0 0-6.74 2.74L3 8"/><path d="M3 3v5h5"/><path d="M3 12a9 9 0 0 0 9 9 9.75 9.75 0 0 0 6.74-2.74L21 16"/><path d="M16 16h5v5"/></svg>';
const deleteicon = obsiIcon2('lucide-eraser', 16);
const gripicon = obsiIcon2('lucide-grip-horizontal', 18);
const upicon = obsiIcon2('lucide-chevrons-up', 16);
const downicon = obsiIcon2('lucide-chevrons-down', 16);

//翻译文本
const I18N = {
  zh: {
    't.title':'对话标题', 't.yulan':'*名字* 预览用',
    't.warn1':'确定要删除吗？', 't.Yes':'确定', 't.No':'取消',
    't.Input':'输入', 't.name1':'样式',
    't.name2':'普通', 't.name3':'属性',
    't.folder1':'图片文件夹', 't.fText1':'(本地用，在线留空) 例：Pic/image/',
    't.folder2':'角色文件夹', 't.fText2':'例：02 素材/随机/对话角色/',
    't.folder3':'笔记文件夹', 't.fText3':'例：03 创作/小说/对话体合集/',
    't.folder4':'笔记模板', 't.fText4':'例：02 素材/模板/对话体模板.md',
    't.notice1':'已设置！', 't.notice3':'文件夹路径有误！',
    't.notice5':'文件路径有误！', 't.name4':'清空勾选',
    't.tag1':'没有标题', 't.tag2':'固定高度', 't.tag3':'变短横线',
    't.tag4':'加外边框', 't.tag5':'没有名字', 't.tag6':'没有头像',
    't.tag7':'无视设定最长宽度', 't.tag8':'鼠标悬停变小手',
    't.tag9':'html标签', 't.tag21':'无折叠', 't.tag22':'折叠展开',
    't.tag23':'折叠收拢', 't.tag31':'无', 't.tag32':'全部',
    't.tag33':'排序', 't.tag34':'顺序↑', 't.tag35':'倒序↓',
    't.tag36':'名字↑', 't.tag37':'名字↓', 't.tag38':'表情↑',
    't.tag39':'表情↓', 't.name10':'每页显示数量', 't.name11':'筛选',
    't.name12':'标题', 't.name13':'key -/+范围', 't.name14':'搜索',
    't.page1':'跳转页数', 't.group1':'角色:', 't.group2':'表情:',
    't.group3':'性别:', 't.group4':'分组:', 't.group5':'角色: ',
    't.group6':'表情: ', 't.group7':'性别: ', 't.group8':'分组: ',
    't.group9':'搜角色: ', 't.group10':'搜表情: ',
    't.group11':'搜分组: ', 't.tip1':'删除筛选条件',
    't.notice6':'没有关键词！', 't.notice7':'没有数据！',
    't.page2':'上一页', 't.page3':'下一页',
    't.page4':'第', 't.page5':'页', 't.page6':'共', 't.page7':'个',
    't.page8':'返回首页', 't.tip2':'替换所选角色',
    't.tip3':'生成角色对话框', 't.tip4':'置顶',
    't.tip5':'取消置顶', 't.name5':'文件夹',
    't.name6':'角色选择', 't.name7':'对话框',
    't.name8':'短链接', 't.tip6':'本地图片和上一篇链接为最短链接',
    't.tip7':'显示/隐藏', 't.name9':'旁白',
    't.tip8':'替换角色', 't.tip9':'移动到上一行',
    't.tip10':'移动到下一行', 't.tip11':'删除此对话生成框',
    't.tip12':'删除全部对话生成框', 't.tip13':'拖动排序',
    't.tip14':'反向', 't.tip15':'插入/替换',
    't.tip16':'插入', 't.tip17':'替换',
    't.tip18':'行数', 't.tip19':'末尾',
    't.notice8':'没有内容！', 't.tip20':'加粗',
    't.tip21':'斜体', 't.tip22':'高亮',
    't.tip23':'删除线', 't.tip24':'文本换行',
    't.tip25':'删除这一行', 't.tip26':'复制这一行',
    't.tip27':'作为对话输入', 't.tip28':'清空重置',
    't.name15':'编辑框', 't.name16':'代码框',
    't.tip29':'保存进YAML', 't.notice9':'已存档！',
    't.tip30':'读取YAML存档', 't.notice10':'已读取数据！',
    't.tip32':'清除保存数据', 't.notice11':'已清除数据！',
    't.tip31':'生成笔记', 't.notice12':'笔记文件夹路径有误！',
    't.notice13':'文件已存在！', 't.notice15':'已生成笔记！',
    't.notice14':'找不到模板！\n将生成无模板笔记',
    'c.width':'6rem',
  },
  en: {
    't.title':'Chat Title', 't.yulan':'*Name* preview',
    't.warn1':'Confirm deletion?', 't.Yes':'Yes', 't.No':'No',
    't.Input':'Input', 't.name1':'Style',
    't.name2':'Normal', 't.name3':'Tag',
    't.folder1':'Image Folder', 't.fText1':'(Local use, leave blank for online) e.g. Pic/image/',
    't.folder2':'Chara Folder', 't.fText2':'e.g. 02 Assets/Random/Dialogue Characters/',
    't.folder3':'Note Folder', 't.fText3':'e.g. 03 Creation/Novel/Dialogue Collection/',
    't.folder4':'Note Template', 't.fText4':'e.g. 02 Assets/Templates/Dialogue Template.md',
    't.notice1':'Saved!', 't.notice3':'Invalid folder path!',
    't.notice5':'Invalid file path!', 't.name4':'Clear Selection',
    't.tag1':'No Title', 't.tag2':'Fixed Height', 't.tag3':'Short Dash',
    't.tag4':'Add Border', 't.tag5':'No Name', 't.tag6':'No Avatar',
    't.tag7':'Max Width(Enforced)', 't.tag8':'Cursor Pointer',
    't.tag9':'Html Tag', 't.tag21':'No Collapse', 't.tag22':'Expand',
    't.tag23':'Collapse', 't.tag31':'None', 't.tag32':'All',
    't.tag33':'Sort', 't.tag34':'Order↑', 't.tag35':'Reverse↓',
    't.tag36':'Name↑', 't.tag37':'Name↓', 't.tag38':'Expression↑',
    't.tag39':'Expression↓', 't.name10':'Per Page', 't.name11':'Filter',
    't.name12':'Title', 't.name13':'Key -/+Range', 't.name14':'Search',
    't.page1':'Go to Page', 't.group1':'Character:', 't.group2':'Expression:',
    't.group3':'Gender:', 't.group4':'Group:', 't.group5':'Character: ',
    't.group6':'Expression: ', 't.group7':'Gender: ', 't.group8':'Group: ',
    't.group9':'Search Character: ', 't.group10':'Search Expression: ',
    't.group11':'Search Group: ', 't.tip1':'Remove Filter',
    't.notice6':'No keyword!', 't.notice7':'No data!',
    't.page2':'Previous', 't.page3':'Next',
    't.page4':'Page: ', 't.page5':'', 't.page6':'Total: ', 't.page7':'',
    't.page8':'First Page', 't.tip2':'Replace Character',
    't.tip3':'Generate Dialog', 't.tip4':'Pin',
    't.tip5':'Unpin', 't.name5':'Folder',
    't.name6':'Character Select', 't.name7':'Dialog',
    't.name8':'Short Link', 't.tip6':'Shortest for local images & prev links',
    't.tip7':'Show/Hide ', 't.name9':'Narration',
    't.tip8':'Replace Char', 't.tip9':'Move Up',
    't.tip10':'Move Down', 't.tip11':'Remove This Dialog',
    't.tip12':'Remove All Dialogs', 't.tip13':'Drag to Sort',
    't.tip14':'Reverse', 't.tip15':'Insert/Replace',
    't.tip16':'Insert', 't.tip17':'Replace',
    't.tip18':'Lines', 't.tip19':'End',
    't.notice8':'No content!', 't.tip20':'Bold',
    't.tip21':'Italic', 't.tip22':'Highlight',
    't.tip23':'Strikethrough', 't.tip24':'Word Wrap',
    't.tip25':'Delete Row', 't.tip26':'Copy Row',
    't.tip27':'Input as Dialog', 't.tip28':'Clear & Reset',
    't.name15':'Edit Box', 't.name16':'Code Box',
    't.tip29':'Save to YAML', 't.notice9':'Archived!',
    't.tip30':'Load from YAML', 't.notice10':'Data loaded!',
    't.tip32':'Clear Saved Data', 't.notice11':'Data cleared!',
    't.tip31':'Generate Note', 't.notice12':'Invalid note folder path!',
    't.notice13':'File already exists!', 't.notice15':'Note generated!',
    't.notice14':'Template not found!\nGenerating note without template',
    'c.width':'7.5rem',
  }
};

function t(key, vars) {
  let s = (I18N[lang] || I18N.zh)[key];
  if (s === undefined) s = key;
  if (vars) {
    for (const [k, v] of Object.entries(vars)) {
      s = s.split('{' + k + '}').join(v);
    }
  }
  return s;
}
document.body.style.setProperty('--chat-inputbox-min-width', t('c.width'));
function applyLang() {
  document.querySelectorAll('[data-i18n]').forEach(el => {
    const key = el.dataset.i18n;
    const val = t(key);
    if (el.tagName === 'INPUT' || el.tagName === 'TEXTAREA') {
      if (el.placeholder !== undefined) el.placeholder = val;
    } else if (el.tagName === 'OPTION') {
      el.textContent = val;
    } else {
      el.textContent = val;
    }
  });
}

// 默认设置
let chatstyle = '> [!chatbox]+ ';
let titletext = t('t.title');
const yulanurl = 'data:image/svg+xml,' + encodeURIComponent(personicon);
const yulan = `\n\> - ![face|100](${yulanurl}) ` + t('t.yulan') + `\n\> + ![face|100](${yulanurl}) ` + t('t.yulan');
const errorurl = 'data:image/svg+xml,' + encodeURIComponent(erroricon);
let textlog = [];
let textshow = [];
let newtext = '';
if (!textlog[0]) {newtext = yulan};
let yulantext = chatstyle + titletext + newtext;
let result1 = '```markdown\n' + chatstyle + titletext + '\n```';
let result2 = chatstyle + titletext;
const filemeta = dv.current().file.frontmatter;
const savefile = this.app.vault.getAbstractFileByPath(dv.current().file.path);
picfolder = filemeta.picfolder;
charafolder = filemeta.charafolder;
notefolder = filemeta.notefolder;
templatePath = filemeta.templatePath;
let showchecknum = [0, 0, 0, 0, 0];
let showchecknum2 = [0, 0];
let piclink = '';
let checknum = [];
for (var i = 0; i <= 8; i++) {
  checknum.push(0);
}
let radionum = 0;
let radionum2 = 1;
let facenum = [];
let facenum2 = null;
let charanum = [];
let chattemp = '';
let mdtitle = '';
let mdalias = '';
let creatTime = '';
let draggedItem = null;
let draggedItem2 = null;
let sureResult = 0;
let idtemp = null;
let indextemp = null;
let codechatON = false;

// 读取本地数据
if (localStorage.hasOwnProperty('chatShowchecknum')) {
  chattemp = localStorage.getItem('chatShowchecknum');
  if (chattemp !== "[]" && chattemp !== "") {
    showchecknum = JSON.parse(chattemp);
  }
}
if (showchecknum[4] !== 0) {piclink = picfolder}

if (localStorage.hasOwnProperty('chatShowchecknum2')) {
  chattemp = localStorage.getItem('chatShowchecknum2');
  if (chattemp !== "[]" && chattemp !== "") {
    showchecknum2 = JSON.parse(chattemp);
  }
}

if (localStorage.hasOwnProperty('chatResult2')) {
  result2 = localStorage.getItem('chatResult2')}

// 检测是否空值
function empty(e) {
  if (/^[\s\u3000\r\n]*$/.test(e)) {return true;
  } else {
    switch (e) {
      case "":
      case "-":
      case ">":
      case null:
      case false:
      case undefined:
        return true;
      default:
        return false;
    }
  }
}

// 增加位数0
function fix(num, length) {
  return ('' + num).length < length ? ((new Array(length + 1)).join('0') + num).slice(-length) : '' + num;
}
// 生成随机4位英数字
function randomString() {
  return Array.from({length: 4}, () => Math.random().toString(36).charAt(2)).join('');
}

// 生成icon
function obsiIcon(iconid, size) {
  const icon = document.createElement('span');
  obsidian.setIcon(icon, iconid);
  icon.classList.add('chat-icon-resize');
  icon.style.setProperty('--icon-svg-width', `${size}px`);
  return icon.outerHTML;
}
function obsiIcon2(iconid, size) {
  const icon = document.createElement('span');
  obsidian.setIcon(icon, iconid);
  icon.classList.add('chat-icon-resize');
  icon.style.setProperty('--icon-svg-width', `${size}px`);
  icon.classList.add('chat-icon-center');
  return icon.outerHTML;
}

// 储存读取yaml
async function savemeta() {
  await app.fileManager.processFrontMatter(savefile, fm => {
    fm.picfolder = picfolder;
    fm.charafolder = charafolder;
    fm.notefolder = notefolder;
    fm.templatePath = templatePath;
  });
}
async function clearmeta() {
  await app.fileManager.processFrontMatter(savefile, fm => {
    fm.result2 = "";
    fm.favid = [];
    fm.charanum = [];
  });
}

// 生成粗体文字
function textnode(text) {
  const divElement = document.createElement("span");
  divElement.style.fontWeight = 'bold';
  divElement.textContent = text;
  return divElement;
}

// 生成标签
function createLabel(forId, text) {
  const label = document.createElement('label');
  label.htmlFor = forId;
  label.appendChild(document.createTextNode(text));
  return label;
}

// 清除最后2个span
const removeSpan = () => {
  this.container.lastChild.remove();
  this.container.lastChild.remove();
}

// 插入目标元素后面
function insertAfter(newElement, targetElement) {
  var parent = targetElement.parentNode;
  if (parent.lastChild === targetElement) {
    parent.appendChild(newElement);
  } else {
    parent.insertBefore(newElement, targetElement.nextSibling);
  }
}

//生成选择按钮
function seleBut(seleTitle, seleUl, cssDiv, cssTitle, titleLabel) {
  const selediv = document.createElement("label");
  selediv.classList.add(cssDiv);
  const seleCheck = document.createElement('input');
  seleCheck.type = 'checkbox';
  seleCheck.checked = false;
  const id = randomString();
  seleCheck.id = id;
  seleCheck.classList.add('chat-Check-up');
  seleTitle.classList.add(cssTitle);
  seleTitle.ariaLabel = titleLabel;
  seleTitle.addEventListener('mouseenter', () => {
    const seleFalse = document.getElementById(id);
    seleFalse.checked = false;
  });
  seleUl.classList.add('newMenu-up-chat');
  selediv.append(seleCheck, seleTitle, seleUl);
  return selediv;
}
function seleBut2(seleTitle, seleUl, cssDiv, cssTitle, titleLabel) {
  const selediv = document.createElement("label");
  selediv.classList.add(cssDiv);
  const seleCheck = document.createElement('input');
  seleCheck.type = 'checkbox';
  seleCheck.checked = false;
  const id = randomString();
  seleCheck.id = id;
  seleCheck.classList.add('chat-Check-down');
  seleTitle.classList.add(cssTitle);
  seleTitle.ariaLabel = titleLabel;
  seleTitle.addEventListener('mouseenter', () => {
    const seleFalse2 = document.getElementById(id);
    seleFalse2.checked = false;
  });
  seleUl.classList.add('newMenu-down-chat');
  selediv.append(seleCheck, seleTitle, seleUl);
  return selediv;
}

// 确认框
const surebox = document.createElement('div');
surebox.classList.add('chat-sureboxdiv');
surebox.style.display = 'none';
const textsure = document.createElement('div');
textsure.classList.add('chat-suretext');
textsure.innerHTML = obsiIcon('lucide-triangle-alert', 24) + t('t.warn1');
const yesnobox = document.createElement('div');
yesnobox.classList.add('chat-yesnobox');
const yesbut = document.createElement('div');
yesbut.classList.add('chat-surebut');
yesbut.textContent = t('t.Yes');
yesbut.onclick = ()=> {
  surebox.style.display = 'none';
  if (sureResult === 1) {
    const value = charanum[idtemp];
    if (facenum2 === value.id) {facenum2 = null}
    charanum.splice(idtemp, 1);
    localStorage.setItem('chatCharanum', JSON.stringify(charanum));
    if (showchecknum[2] === 0) {fy()};
    chatWordDiv.removeChild(chatWordDiv.children[idtemp]);
  } else if (sureResult === 2) {
    textlog.splice(indextemp,1);
    editdiv.removeChild(editdiv.children[indextemp]);
    changelistnum();
    if (facenum.length >= 1) {
      if (facenum.includes(indextemp)) {
        const delenum = facenum.indexOf(indextemp);
        facenum.splice(delenum,1);
        if (facenum.length < 1) {
          if (showchecknum[2] === 0) {fy()};
        }
      }
      if (facenum.length >= 1) {
        facenum.forEach((p, index) => {
          if (p > indextemp) {
            facenum[index] = p - 1;
          }
        });
      }
    }
    styleword();
    codeRefresh();
  } else if (sureResult === 3) {
    resetCode();
    styleword();
    if (showchecknum2[0] === 1) {editframe()};
    result2 = '';
    localStorage.setItem("chatResult2", result2);
    codeRefresh();
  } else if (sureResult === 4) {
    chatWordDiv.innerHTML = "";
    facenum2 = null;
    charanum = [];
    localStorage.setItem('chatCharanum', JSON.stringify(charanum));
    if (showchecknum[2] === 0) {fy()};
  }
  sureResult = 0;
};
const nobut = document.createElement('div');
nobut.classList.add('chat-surebut');
nobut.textContent = t('t.No');
nobut.onclick = ()=> {surebox.style.display = 'none'};
yesnobox.append(yesbut, nobut);
surebox.append(textsure, yesnobox);

// 输入文件夹数据
function crfolder(css, text, placetext, path, num) {
  const folderContainer = document.createElement("div");
  folderContainer.classList.add(css);
  const foldertext = document.createElement('span');
  foldertext.textContent = text;
  foldertext.classList.add('chat-folder-title');
  folderContainer.appendChild(foldertext);
  const inputfolder = document.createElement("input");
  inputfolder.type = "text";
  inputfolder.placeholder = placetext;
  inputfolder.classList.add('chat-inputtitle');
  inputfolder.value = path;
  const folderbut = document.createElement("span");
  folderbut.innerHTML = penicon;
  folderbut.ariaLabel = t('t.Input');
  folderbut.classList.add('chat-folder-button');
  folderbut.onclick = ()=> {
    if (num !== 4) {
      folderRoute(inputfolder.value, num);
    } else {
      fileRoute(inputfolder.value)
    }
    inputfolder.value = path;
  }
  folderContainer.append(inputfolder, folderbut);

  inputfolder.addEventListener('keydown', function(event) {
    if (event.key === 'Enter' || event.code === 'Enter') {
      this.blur();
      if (num !== 4) {
        folderRoute(inputfolder.value, num);
      } else {
        fileRoute(inputfolder.value)
      }
      inputfolder.value = path;
    }
  });
  inputfolder.addEventListener('blur', function() {
    if (num !== 4) {
      folderRoute(inputfolder.value, num);
    } else {
      fileRoute(inputfolder.value)
    }
    inputfolder.value = path;
  });
  return folderContainer
}

const folderContainer1 = crfolder('chat-folder-div', t('t.folder1'), t('t.fText1'), picfolder, 1);
const folderContainer2 = crfolder('chat-folder-div', t('t.folder2'), t('t.fText2'), charafolder, 2);
const folderContainer3 = crfolder('chat-folder-div', t('t.folder3'), t('t.fText3'), notefolder, 3);
const folderContainer4 = crfolder('chat-folder-div2', t('t.folder4'), t('t.fText4'), templatePath, 4);

function checkRoute(value) {
  const text = value.substring(value.length - 1);
  if (text !== '/') {return value + '/';
  } else {return value}
}

async function folderRoute(value, num) {
  if (empty(value)) {
    if (num === 1) {
      picfolder = '';
      if (showchecknum[4] !== 0) {piclink = picfolder}
    } else if (num === 2) {
      charafolder = '';
    } else if (num === 3) {
      notefolder = '';
    }
    savemeta();
    new obsidian.Notice(t('t.notice1'));
  } else {
    const checkpath = checkRoute(value);
    const folderExists2 = await app.vault.adapter.exists(checkpath);
    if (!folderExists2) {
      new obsidian.Notice(t('t.notice3'));
    } else {
      if (num === 1) {
        picfolder = checkpath;
        if (showchecknum[4] !== 0) {piclink = picfolder}
      } else if (num === 2) {
        charafolder = checkpath;
      } else if (num === 3) {
        notefolder = checkpath;
      }
      savemeta();
      new obsidian.Notice(t('t.notice1'));
    }
  }
}

async function fileRoute(value) {
  if (empty(value)) {
    templatePath = '';
    savemeta();
    new obsidian.Notice(t('t.notice1'));
  } else {
    const text = value.substring(value.length - 3);
    let mdpath = value;
    if (text !== '.md') {mdpath = value + '.md';}
    const fileExists2 = await app.vault.adapter.exists(mdpath);
    if (!fileExists2) {
      new obsidian.Notice(t('t.notice5'));
    } else {
      templatePath = mdpath;
      savemeta();
      new obsidian.Notice(t('t.notice1'));
    }
  }
}

// 样式单选框
function createRadio(id, name, value, num) {
  const radio = document.createElement('input');
  radio.type = 'radio';
  radio.name = name; // 确保单选按钮属于同一组
  radio.id = id;
  radio.value = value;
  radio.addEventListener('change', function() {
    if (num === 0) {
      const idindex = this.id.replace(/radio/g, '');
      radionum = Number(idindex);
    } else {
      const idindex2 = this.id.replace(/radio2/g, '');
      radionum2 = Number(idindex2);
    }
    styleword();
    codeRefresh();
  });
  return radio;
}

const radioContainer = document.createElement("div");
radioContainer.classList.add('chat-folder-div4');
const radiotext = document.createElement('span');
radiotext.textContent = t('t.name1');
radiotext.classList.add('chat-folder-title3');
radioContainer.appendChild(radiotext);
const radioinner = document.createElement('div');
radioinner.classList.add('chat-folder-inner');
radioContainer.appendChild(radioinner);
const options = [t('t.name2'), 'bbs', 'pop', 'wechat', 'qqchat', 'linshe', 'baker'];
options.forEach(function(option, index) {
  const radio = createRadio('radio' + index, 'radioGroup', option, 0);
  const label1 = createLabel('radio' + index, option);
  if (radionum === index) {
    radio.checked = true;
  }
  label1.classList.add('chat-label1');
  radioinner.append(radio, label1);
});

// 属性多选框
function createCheckbox(id, name, value) {
  const checkbox = document.createElement('input');
  checkbox.type = 'checkbox';
  checkbox.id = id;
  checkbox.name = name;
  checkbox.value = value;
  return checkbox;
}

// 创建并添加多个勾选框到页面
const checkdiv = document.createElement("div");
checkdiv.classList.add('chat-checkdiv');
const checktext = document.createElement('span');
checktext.textContent = t('t.name3');
checktext.classList.add('chat-folder-title3');
checkdiv.appendChild(checktext);
const checkContainer = document.createElement("div");
const checkcon1 = document.createElement("div");
checkcon1.classList.add('chat-folder-inner');
const checkcon2 = document.createElement("div");
checkcon2.classList.add('chat-folder-inner');

const options2 = ['notitle', 'fix', 'short', 'frame', 'noname', 'noface', 'long', 'point', 'htmltag'];
const options2cn = [t('t.tag1'), t('t.tag2'), t('t.tag3'), t('t.tag4'), t('t.tag5'), t('t.tag6'), t('t.tag7'), t('t.tag8'), t('t.tag9')];
options2.forEach(function(option, index) {
  const labtext = options2cn[index];
  const checkbox = createCheckbox('checkbox' + index, labtext, option);
  const label = createLabel('checkbox' + index, labtext);
  if (checknum[index] === 1) {
    checkbox.checked = true;
  }
  label.classList.add('chat-label2');
  if (index <= 4) {
    checkcon1.append(checkbox, label);
  } else {
    checkcon2.append(checkbox, label);
  }
});
const clearcheck = document.createElement("span");
clearcheck.innerHTML = deleteicon;
clearcheck.ariaLabel = t('t.name4');
clearcheck.classList.add('chat-folder-button3');
clearcheck.onclick = ()=> {
  for (var i = 0; i <=8; i++) {
    const allchecks = document.getElementById(`checkbox${i}`);
    allchecks.checked = false;
    checknum[i] = 0;
  }
  styleword();
  codeRefresh();
}
checkContainer.append(checkcon1, checkcon2);
checkdiv.append(checkContainer, clearcheck);

//多选框监听
checkContainer.addEventListener('change', function(event) {
  if (event.target.type === 'checkbox') {
    const checkidnum2 = event.target.id.replace(/checkbox/g, '');
    const checkidnum = Number(checkidnum2);
    if (event.target.checked) {
      checknum[checkidnum] = 1;
    } else {
      checknum[checkidnum] = 0;
    }
    styleword();
    codeRefresh();
  }
});

// 标题单选框
const radio2Container = document.createElement("div");
radio2Container.classList.add('chat-folder-div5');
const radio2text = document.createElement('span');
radio2text.textContent = t('t.name12');
radio2text.classList.add('chat-folder-title3');
radio2Container.appendChild(radio2text);
const radioinner2 = document.createElement('div');
radioinner2.classList.add('chat-folder-inner2');
radio2Container.appendChild(radioinner2);
const options3 = [t('t.tag21'), t('t.tag22'), t('t.tag23')];
options3.forEach(function(option, index) {
  const radio2 = createRadio('radio2' + index, 'radioGroup2', option, 1);
  const label3 = createLabel('radio2' + index, option);
  if (radionum2 === index) {
    radio2.checked = true;
  }
  label3.classList.add('chat-label1');
  radioinner2.append(radio2, label3);
});

// 标题输入框
const inputTitlediv = document.createElement('div');
inputTitlediv.classList.add('chat-folder-div3');
const inputTitle = document.createElement("input");
inputTitle.type = "text";
inputTitle.placeholder = t('t.title');
inputTitle.classList.add('chat-inputtitle');
const titlebut = document.createElement("span");
titlebut.innerHTML = penicon;
titlebut.ariaLabel = t('t.Input');
titlebut.classList.add('chat-folder-button3');
titlebut.onclick = ()=> {titleinput()}
function titleinput() {
  titletext = inputTitle.value;
  if (empty(titletext)) {
    titletext = '';
    inputTitle.value = '';
    if (checknum[0] === 0) {
      checknum[0] = 1;
      if (showchecknum[0] === 0) {
        const checktitle = document.getElementById('checkbox0');
        checktitle.checked = true;
      };
    }
  } else {
    if (checknum[0] === 1) {
      checknum[0] = 0;
      if (showchecknum[0] === 0) {
        const checktitle = document.getElementById('checkbox0');
        checktitle.checked = false;
      };
    }
  }
  styleword();
  codeRefresh();
}
inputTitlediv.appendChild(inputTitle);
radio2Container.append(inputTitlediv, titlebut);

inputTitle.addEventListener('keydown', function(event) {
  if (event.key === 'Enter' || event.code === 'Enter') {
    this.blur();
    titleinput();
  }
});
inputTitle.addEventListener('blur', function() {
  titleinput();
});

// 角色一览
let charafiles = null;
let allfiles = [];
if (charafolder !== '') {
  charafiles = app.vault.getMarkdownFiles().filter(file => file.path.includes(charafolder)).sort((a, b) => a.name.localeCompare(b.name));
  const cachearr = charafiles.map(async (file) => {
    let characache = await app.vault.cachedRead(file);
    characache = characache.replaceAll('，', ',');
    let line = characache.split("\n")
      .filter(value => !empty(value) && !value.startsWith('//') && /(.*,){4}/.test(value));
    return line;
  });
  await Promise.all(cachearr).then(values => {
    const line3 = values.flat();
    for (var i=0; i < line3.length; i++) {
      let line2 = String(line3[i]).split(",");
      let obj = {};
      obj.id = i;
      obj.chara = line2[0].trim();
      obj.state = line2[1].trim();
      if (empty(obj.state)) {obj.state = t('t.tag31')}
      obj.sex = line2[2].trim();
      if (empty(obj.sex)) {obj.sex = t('t.tag31')}
      obj.group = line2[3].trim();
      if (empty(obj.group)) {obj.group = t('t.tag31')}
      obj.link = line2[4].trim();
      if (empty(obj.link)) {obj.link = t('t.tag31')}
      obj.fav = false;
      allfiles.push(obj);
    }
  })
}

let global = 0;
let listnum = 10;
let tempfiles = allfiles;
let arrfiles = allfiles;
let searcharr = arrfiles;
let files = null;
let charaname = 'All';
let charastate = 'All';
let charasex = 'All';
let charagroup = 'All';
let searchtext = "";
let searchCharaSave = "";
let searchStateSave = "";
let searchGroupSave = "";
let favid = [];

let num = tempfiles.length;
let page = global + 1;
let pageall = Math.ceil(num / listnum);
let sort = 0;
let selenum = 0;
let temparr = [];
let arrchara = [];
let arrstate = [];
let arrsex = [];
let arrgroup = [];

//读取本地数据
if (localStorage.hasOwnProperty('chatListnum')) {
  listnum = Number(localStorage.getItem('chatListnum'));}
if (localStorage.hasOwnProperty('chatSort')) {
  sort = Number(localStorage.getItem('chatSort'));}

if (localStorage.hasOwnProperty('chatFavid')) {
  chattemp = localStorage.getItem('chatFavid');
  if (chattemp !== "[]" && chattemp !== "") {
    favid = JSON.parse(chattemp);
    if (favid.length !== 0) {
      chattemp = favid.filter(function(value) {
        return value < allfiles.length;
      });
      favid = chattemp.slice();
      localStorage.setItem('chatFavid', JSON.stringify(favid));
    }
  }
}

if (localStorage.hasOwnProperty('chatCharanum')) {
  chattemp = localStorage.getItem('chatCharanum');
  if (chattemp !== "[]" && chattemp !== "") {
    charanum = JSON.parse(chattemp);
    if (charanum.length !== 0) {
      chattemp = charanum.filter(function(value) {
        return value.id < allfiles.length;
      });
      charanum = chattemp.slice();
      localStorage.setItem('chatCharanum', JSON.stringify(charanum));
    }
  }
}

async function savemeta2() {
  await app.fileManager.processFrontMatter(savefile, fm => {
    fm.result2 = result2;
    fm.favid = favid;
    fm.charanum = charanum;
  });
}

// 搜索显示框
const seleshow = document.createElement("div");
seleshow.classList.add('my-chat-sele3');
seleshow.innerHTML = "";

// 排序搜索综合框
const seleall = document.createElement("div");
seleall.classList.add('my-chat-sele');

// 排序按钮
const sortDataTitle = document.createElement("div");
const sortDataUl = document.createElement("section");
const sortData = seleBut(sortDataTitle, sortDataUl, 'chat-menubut-up', 'chat-sele-titlexj', t('t.tag33'));

switch (sort) {
  case 0:
    sortDataTitle.textContent = t('t.tag34');
    break;
  case 1:
    sortDataTitle.textContent = t('t.tag35');
    break;
  case 2:
    sortDataTitle.textContent = t('t.tag36');
    break;
  case 3:
    sortDataTitle.textContent = t('t.tag37');
    break;
  case 4:
    sortDataTitle.textContent = t('t.tag38');
    break;
  case 5:
    sortDataTitle.textContent = t('t.tag39');
    break;
  default:
    sortDataTitle.textContent = t('t.tag34');
}

function sortbut(nadiv, inner, numdiv) {
  nadiv = document.createElement("div");
  nadiv.classList.add('my-seleop-chat');
  nadiv.textContent = inner;
  nadiv.onclick = ()=> {
    sort = numdiv;sortDataTitle.textContent = inner;
    localStorage.setItem("chatSort", sort);
    fy()
  }
  return nadiv;
}
sortDataUl.appendChild(sortbut('paixu1', t('t.tag34'), 0));
sortDataUl.appendChild(sortbut('paixu2', t('t.tag35'), 1));
sortDataUl.appendChild(sortbut('paixu3', t('t.tag36'), 2));
sortDataUl.appendChild(sortbut('paixu4', t('t.tag37'), 3));
sortDataUl.appendChild(sortbut('paixu5', t('t.tag38'), 4));
sortDataUl.appendChild(sortbut('paixu6', t('t.tag39'), 5));

// 每页显示按钮
const listDataTitle = document.createElement("div");
const listDataUl = document.createElement("section");
const listData = seleBut(listDataTitle, listDataUl, 'chat-menubut-up', 'chat-sele-titlexj', t('t.name10'));
listDataTitle.textContent = listnum;

function listbut(nadiv, numdiv) {
  nadiv = document.createElement("div");
  nadiv.classList.add('my-seleop-chat');
  nadiv.textContent = numdiv;
  nadiv.onclick = ()=> {
    global = 0;
    listnum = numdiv;listDataTitle.textContent = numdiv;
    localStorage.setItem("chatListnum", listnum);
    pagebut();
    fy()
  }
  return nadiv;
}
listDataUl.appendChild(listbut('list1', 10));
listDataUl.appendChild(listbut('list2', 15));
listDataUl.appendChild(listbut('list3', 20));
listDataUl.appendChild(listbut('list4', 25));
listDataUl.appendChild(listbut('list5', 30));
listDataUl.appendChild(listbut('list6', 35));
listDataUl.appendChild(listbut('list7', 40));
listDataUl.appendChild(listbut('list8', 45));
listDataUl.appendChild(listbut('list9', 50));

// 筛选名称
const selenameTitle = document.createElement("div");
const selenameUl = document.createElement("section");
const selename = seleBut(selenameTitle, selenameUl, 'chat-menubut-up', 'chat-sele-titlexj', t('t.name11'));
selenameTitle.textContent = t('t.tag32');

// 筛选容器
const selenull = document.createElement("div");
selenull.innerHTML = "";
const seleExtraNull = document.createElement("div");
seleExtraNull.classList.add('my-chat-sele3');
seleExtraNull.innerHTML = "";

// 筛选角色名
const selecharaTitle = document.createElement("div");
const selecharaUl = document.createElement("section");
const selechara = seleBut(selecharaTitle, selecharaUl, 'chat-menubut-up', 'chat-sele-title', '');

// 搜索框
const searchdiv = document.createElement('div');
searchdiv.classList.add('chat-searchdiv');
const inputSearch = document.createElement("input");
inputSearch.type = "text";
inputSearch.placeholder = t('t.name13');
inputSearch.classList.add('chat-search-input');
const searchbut = document.createElement("span");
searchbut.innerHTML = obsiIcon2('lucide-search', 18);
searchbut.ariaLabel = t('t.name14');
searchbut.classList.add('chat-searchbut');
searchbut.onclick = ()=> {searchfile()}
searchdiv.append(inputSearch, searchbut);

// 筛选表情
const selestateTitle = document.createElement("div");
const selestateUl = document.createElement("section");
const selestate = seleBut(selestateTitle, selestateUl, 'chat-menubut-up', 'chat-sele-title', '');

// 筛选性别
const selesexTitle = document.createElement("div");
const selesexUl = document.createElement("section");
const selesex = seleBut(selesexTitle, selesexUl, 'chat-menubut-up', 'chat-sele-title', '');

// 筛选分组
const selegroupTitle = document.createElement("div");
const selegroupUl = document.createElement("section");
const selegroup = seleBut(selegroupTitle, selegroupUl, 'chat-menubut-up', 'chat-sele-title', '');

// 跳转页数
const selepageTitle = document.createElement("div");
const selepageUl = document.createElement("section");
const selepage = seleBut(selepageTitle, selepageUl, 'chat-menu-up', 'chat-sele-title2', t('t.page1'));
const selepageTitle2 = document.createElement("div");
const selepageUl2 = document.createElement("section");
const selepage2 = seleBut2(selepageTitle2, selepageUl2, 'chat-menu-down', 'chat-sele-title2', t('t.page1'));

// 筛选名字按钮
function selenamebut(nadiv, inner, numdiv) {
  nadiv = document.createElement("div");
  nadiv.classList.add('my-seleop-chat');
  nadiv.textContent = inner;
  nadiv.onclick = ()=> {
    selenum = numdiv;selenameTitle.textContent = inner;
    selenamediv();
  }
  return nadiv;
}
function selenamediv() {
  selenull.innerHTML = "";
  seleExtraNull.innerHTML = "";
  inputSearch.value = "";
  arrfileset();
  if (selenum === 0) {
    seleshow.innerHTML = "";
    global = 0;
    charaname = 'All';
    charastate = 'All';
    charasex = 'All';
    charagroup = 'All';
    searchtext = "";
    searchCharaSave = "";
    searchStateSave = "";
    searchGroupSave = "";
    tempfiles = allfiles;
    pagebut();
    fy();
  }
  if (selenum === 1) {
    rechara();
    selenull.appendChild(selechara);
    inputSearch.value = searchCharaSave;
    seleExtraNull.appendChild(searchdiv);
    }
  if (selenum === 2) {
    restate();
    selenull.appendChild(selestate);
    inputSearch.value = searchStateSave;
    seleExtraNull.appendChild(searchdiv);
    }
  if (selenum === 3) {
    resex();
    selenull.appendChild(selesex);
    }
  if (selenum === 4) {
    regroup();
    selenull.appendChild(selegroup);
    inputSearch.value = searchGroupSave;
    seleExtraNull.appendChild(searchdiv);
    }
}
selenameUl.appendChild(selenamebut('name0', t('t.tag32'), 0));
selenameUl.appendChild(selenamebut('name1', t('t.group1'), 1));
selenameUl.appendChild(selenamebut('name2', t('t.group2'), 2));
selenameUl.appendChild(selenamebut('name3', t('t.group3'), 3));
selenameUl.appendChild(selenamebut('name4', t('t.group4'), 4));

// 确定files范围
function fileset() {
  tempfiles = allfiles;
  if (charaname !== 'All') {
    tempfiles = tempfiles.filter(t=> String(t.chara).contains(charaname))}
  if (charastate !== 'All') {
    tempfiles = tempfiles.filter(t=> String(t.state).contains(charastate))}
  if (charasex !== 'All') {
    tempfiles = tempfiles.filter(t=> String(t.sex).contains(charasex))}
  if (charagroup !== 'All') {
    tempfiles = tempfiles.filter(t=> String(t.group).contains(charagroup))}

  searcharr = tempfiles;

  if (!empty(searchCharaSave)) {
    tempfiles = searchstr(searchCharaSave, 1);
    searcharr = tempfiles;
  }
  if (!empty(searchStateSave)) {
    tempfiles = searchstr(searchStateSave, 2);
    searcharr = tempfiles;
  }
  if (!empty(searchGroupSave)) {
    tempfiles = searchstr(searchGroupSave, 4);
    searcharr = tempfiles;
  }
  pagebut();
  fileShowset();
};
function fileShowset() {
  seleshow.innerHTML = "";
  let textarr = [];
  let textnumarr = [];
  let seletext = "";
  if (charaname !== 'All') {
    seletext = t('t.group5') + charaname;
    textarr.push(seletext);
    textnumarr.push(1);
  }
  if (charastate !== 'All') {
    seletext = t('t.group6') + charastate;
    textarr.push(seletext);
    textnumarr.push(2);
  }
  if (charasex !== 'All') {
    seletext = t('t.group7') + charasex;
    textarr.push(seletext);
    textnumarr.push(3);
  }
  if (charagroup !== 'All') {
    seletext = t('t.group8') + charagroup;
    textarr.push(seletext);
    textnumarr.push(4);
  }
  if (!empty(searchCharaSave)) {
    seletext = t('t.group9') + searchCharaSave;
    textarr.push(seletext);
    textnumarr.push(1.1);
  }
  if (!empty(searchStateSave)) {
    seletext = t('t.group10') + searchStateSave;
    textarr.push(seletext);
    textnumarr.push(2.1);
  }
  if (!empty(searchGroupSave)) {
    seletext = t('t.group11') + searchGroupSave;
    textarr.push(seletext);
    textnumarr.push(4.1);
  }
  if (!empty(textarr[0])) {
    for (var i=0; i < textarr.length; i++) {
      let textop = document.createElement("span");
      textop.classList.add('my-chat-seletext');
      let num = textnumarr[i];
      textop.innerHTML = textarr[i];
      textop.ariaLabel = t('t.tip1');
      textop.onclick = ()=> {
        global = 0;
        if (num === 1) {charaname = 'All'}
        if (num === 1.1) {searchCharaSave = ""}
        if (num === 2) {charastate = 'All'}
        if (num === 2.1) {searchStateSave = ""}
        if (num === 3) {charasex = 'All'}
        if (num === 4) {charagroup = 'All'}
        if (num === 4.1) {searchGroupSave = ""}
        selenamediv();
        fileset();
        fy();
      }
      seleshow.appendChild(textop);
    }
  }
};
function arrfileset() {
  arrfiles = allfiles;
  if (selenum === 0) {
    arrfiles = allfiles;
  } else {
    if (selenum !== 1) {
      if (charaname !== "All") {
        arrfiles = arrfiles.filter(t=> String(t.chara).contains(charaname))}
      searcharr = arrfiles;
      if (!empty(searchCharaSave)) {
        arrfiles = searchstr(searchCharaSave, 1);}
    }
    if (selenum !== 2) {
      if (charastate !== "All") {
        arrfiles = arrfiles.filter(t=> String(t.state).contains(charastate))}
      searcharr = arrfiles;
      if (!empty(searchStateSave)) {
        arrfiles = searchstr(searchStateSave, 2);}
    }
    if (selenum !== 3) {
      if (charasex !== "All") {
        arrfiles = arrfiles.filter(t=> String(t.sex).contains(charasex))}
    }
    if (selenum !== 4) {
      if (charagroup !== "All") {
        arrfiles = arrfiles.filter(t=> String(t.group).contains(charagroup))}
      searcharr = arrfiles;
      if (!empty(searchGroupSave)) {
        arrfiles = searchstr(searchGroupSave, 4);}
    }
  }
  searcharr = arrfiles;
};

//菜单排序
function menusort(arr, item) {
  const copy = [...arr];
  copy.sort((a, b) => {
    let nameA = arrfiles.filter(t=> String(t[item]).contains(a[item])).length;
    let nameB = arrfiles.filter(t=> String(t[item]).contains(b[item])).length;
    return nameA < nameB ? 1 : nameA > nameB ? -1 : 0;
  });
  return copy;
}

function menusort2(arr, item) {
  const copy = [...arr];
  copy.sort((a, b) => {
    let nameA = arrfiles.filter(t=> String(t[item]).contains(a)).length;
    let nameB = arrfiles.filter(t=> String(t[item]).contains(b)).length;
    return nameA < nameB ? 1 : nameA > nameB ? -1 : 0;
  });
  return copy;
}

// 重置角色按钮
function rechara() {
  selecharaUl.innerHTML = "";
  if (charaname === "All") {selecharaTitle.textContent = t('t.tag32');}
  temparr = menusort(arrfiles, 'chara');
  temparr = temparr.map(obj => {return obj.chara;})
  arrchara = Array.from(new Set(temparr));
  arrchara.unshift('All');
  arrchara.map((p, index) => {
    if (!empty(p)) {
      let selecharaop = document.createElement("div");
    selecharaop.classList.add('my-seleop-chat');
    let opnum = arrfiles.filter(t=> String(t.chara).contains(p)).length;
    if (index === 0) {opnum = arrfiles.length;} else if (charaname === p) {
      selecharaTitle.textContent = p;
    }
    selecharaop.innerHTML = p + " "+ opnum;
    selecharaop.onclick = ()=> {
      selecharaTitle.textContent = p;
      global = 0;
      charaname = p;
      searchCharaSave = "";
      inputSearch.value = "";
      fileset();
      fy();
    }
    selecharaUl.appendChild(selecharaop);
    }
  })
};

// 重置表情按钮
function restate() {
  selestateUl.innerHTML = "";
  if (charastate === "All") {selestateTitle.textContent = t('t.tag32');}
  temparr = menusort(arrfiles, 'state');
  temparr = temparr.map(obj => {return obj.state;})
  arrstate = Array.from(new Set(temparr));
  arrstate.unshift('All');
  arrstate.map((p, index) => {
    let selestateop = document.createElement("div");
    selestateop.classList.add('my-seleop-chat');
    let opnum = arrfiles.filter(t=> String(t.state).contains(p)).length;
    if (index === 0) {opnum = arrfiles.length;} else if (charastate === p) {
      selestateTitle.textContent = p;
    }
    selestateop.innerHTML = p + " "+ opnum;
    selestateop.onclick = ()=> {
      selestateTitle.textContent = p;
      global = 0;
      charastate = p;
      searchStateSave = "";
      inputSearch.value = "";
      fileset();
      fy();
    }
    selestateUl.appendChild(selestateop);
  })
};

// 重置性别按钮
function resex() {
  selesexUl.innerHTML = "";
  if (charasex === "All") {selesexTitle.textContent = t('t.tag32');}
  temparr = menusort(arrfiles, 'sex');
  temparr = temparr.map(obj => {return obj.sex;})
  arrsex = Array.from(new Set(temparr));
  arrsex.unshift('All');
  arrsex.map((p, index) => {
    let selesexop = document.createElement("div");
    selesexop.classList.add('my-seleop-chat');
    let opnum = arrfiles.filter(t=> String(t.sex).contains(p)).length;
    if (index === 0) {opnum = arrfiles.length;} else if (charasex === p) {
      selesexTitle.textContent = p;
    }
    selesexop.innerHTML = p + " "+ opnum;
    selesexop.onclick = ()=> {
      selesexTitle.textContent = p;
      global = 0;
      charasex = p;
      fileset();
      fy();
    }
    selesexUl.appendChild(selesexop);
  })
};

// 重置分组按钮
function regroup() {
  selegroupUl.innerHTML = "";
  if (charagroup === "All") {selegroupTitle.textContent = t('t.tag32');}
  temparr = [];
  arrfiles.map(p => {
    let line3 = p.group.replaceAll('、', ';');
    line3 = line3.split(";");
    for (var i=0; i < line3.length; i++) {
      temparr.push(line3[i])
    }
  });
  temparr = menusort2(temparr, 'group');
  arrgroup = Array.from(new Set(temparr));
  arrgroup.unshift('All');
  arrgroup.map((p, index) => {
    let selegroupop = document.createElement("div");
    selegroupop.classList.add('my-seleop-chat');
    let opnum = arrfiles.filter(t=> String(t.group).contains(p)).length;
    if (index === 0) {opnum = arrfiles.length;} else if (charagroup === p) {
      selegroupTitle.textContent = p;
    }
    selegroupop.innerHTML = p + " "+ opnum;
    selegroupop.onclick = ()=> {
      selegroupTitle.textContent = p;
      global = 0;
      charagroup = p;
      searchGroupSave = "";
      inputSearch.value = "";
      fileset();
      fy();
    }
    selegroupUl.appendChild(selegroupop);
  })
};

// 搜索功能
function searchfile() {
  searchtext = inputSearch.value;
  if (empty(searchtext)) {
    new obsidian.Notice(t('t.notice6'), 3000);
  } else {
    searchtext = searchstr(searchtext, selenum);
    if (searchtext) {
      global = 0;
      tempfiles = searchtext;
      searchtext = "";
      pagebut();
      fileShowset();
      fy();
    }
  }
}

function searchstr(str, num) {
  const matchtext = str.match(/[^\s]+/g);
  function namesele(t) {
    if (num === 1) {
      return t.chara;
    }
    if (num === 2) {
      return t.state;
    }
    if (num === 4) {
      return t.group;
    }
  }
  let searchfiles = searcharr;
  if (!empty(matchtext)) {
    matchtext.map(p => {
      if (!p.startsWith('+') && !p.startsWith('-')) {
        p = p.replace(/"|'/g, '');
        searchfiles = searchfiles.filter(t => {
          const filename = namesele(t);
          return String(filename).toLowerCase().includes(p.toLowerCase());
        });
      }
    })
  }
  if (!empty(matchtext)) {
    matchtext.map(p => {
      if (p.startsWith('+')) {
        p = p.replace(/"|'/g, '');
        p = p.slice(1);
        const addarr = searcharr.filter(t => {
          const filename = namesele(t);
          return String(filename).toLowerCase().includes(p.toLowerCase());
        });
        searchfiles = searchfiles.concat(addarr);
      }
    })
    const temparr2 = Array.from(new Set(searchfiles));
    searchfiles = temparr2;
  }
  if (!empty(matchtext)) {
    matchtext.map(p => {
      if (p.startsWith('-')) {
        p = p.replace(/"|'/g, '');
        p = p.slice(1);
        searchfiles = searchfiles.filter(t => {
          const filename = namesele(t);
          return !String(filename).toLowerCase().includes(p.toLowerCase());
        });
      }
    })
  }
  if (!empty(searchfiles[0])) {
    if (num === 1) {
      searchCharaSave = str;
    }
    if (num === 2) {
      searchStateSave = str;
    }
    if (num === 4) {
      searchGroupSave = str;
    }
    return searchfiles;
  } else {
    new obsidian.Notice(t('t.notice7'), 3000);
    return false;
  }
}

// 导航按钮
const allnum = document.createElement("span");
const allnum2 = document.createElement("span");
function daohangbut(divname1, divnametitle1, divname2, classname) {
  const prev = document.createElement("span");
  prev.textContent = "◁";
  prev.ariaLabel = t('t.page2');
  prev.classList.add('my-text-chat');
  prev.onclick = ()=> {
    if (global > 0) {global -= 1;fy()
    } else if ((global === 0) && (num !== 0) && (pageall !== 1)) {global = pageall - 1;fy()}
  }
  const next = document.createElement("span");
  next.textContent = "▷";
  next.ariaLabel = t('t.page3');
  next.classList.add('my-text-chat');
  next.onclick = ()=> {
    if ( (global+1)*listnum < num) {
      global += 1;fy()
    } else if ((num !== 0) && (pageall !== 1)) {global = 0;fy()}
  }
  divnametitle1.innerHTML = t('t.page4') + page + "/" + pageall + t('t.page5');
  divname2.innerHTML = t('t.page6') + num + t('t.page7');
  divname2.classList.add('my-text-chat');
  divname2.ariaLabel = t('t.page8');
  divname2.onclick = ()=> {global = 0;fy()}
  const daohang = document.createElement("div");
  daohang.classList.add(classname);
  daohang.append(prev, divname1, divname2, next);
  return daohang;
}
function pagenum() {
  page = global + 1;
  num = tempfiles.length;
  if (num === 0) {page = 0;}
  pageall = Math.ceil(num / listnum);
  selepageTitle.innerHTML = t('t.page4') + page + "/" + pageall + t('t.page5');
  selepageTitle2.innerHTML = t('t.page4') + page + "/" + pageall + t('t.page5');
  allnum.innerHTML = t('t.page6') + num + t('t.page7');
  allnum2.innerHTML = t('t.page6') + num + t('t.page7');
}

// 重置页数按钮
function pagebut() {
  selepageUl.innerHTML = "";
  selepageUl2.innerHTML = "";
  pagenum();
  for (var i = 0; i < pageall; i++) {
    let pageopbut = document.createElement("div");
    pageopbut.classList.add('my-seleop-chat');
    let numop = i+1;
    let pagei = i;
    pageopbut.innerHTML = t('t.page4') + numop + t('t.page5');
    pageopbut.onclick = ()=> {
      global = pagei;
      fy()
    }
    selepageUl.appendChild(pageopbut);
  }
  for (var i2 = 0; i2 < pageall; i2++) {
    let pageopbut2 = document.createElement("div");
    pageopbut2.classList.add('my-seleop-chat');
    let numop2 = i2+1;
    let pagei2 = i2;
    pageopbut2.innerHTML = t('t.page4') + numop2 + t('t.page5');
    pageopbut2.onclick = ()=> {
      global = pagei2;
      fy()
    }
    selepageUl2.appendChild(pageopbut2);
  }
};pagebut();

// 排序
function getPriority(char) {
  if (/\d/.test(char)) return 1; // 数字
  if (/[a-zA-Z]/.test(char)) return 2; // 英文
  if (/[\u4e00-\u9fa5]/.test(char)) return 3; // 汉字
  return 0; // 其他字符，可以根据需要调整
}
function sortNames(names, item) {
  return names.sort((a, b) => {
    let nameA = a[item].split('');
    let nameB = b[item].split('');
    for (let i = 0; i < Math.max(nameA.length, nameB.length); i++) {
      let charA = nameA[i] || '';
      let charB = nameB[i] || '';
      let priorityA = getPriority(charA);
      let priorityB = getPriority(charB);
      if (priorityA !== priorityB) {
        return priorityA - priorityB;
      } else if (nameA[i] !== nameB[i]) {
        return nameA[i].localeCompare(nameB[i]);
      }
    }
    return 0; // 如果所有字符都相同，则认为两个名字相等
  });
}

function sort1(fileB) {
  let fileA = fileB.slice();
  if (sort === 1) {fileA = fileB.slice().reverse()};
  if (sort === 2) {fileA = sortNames(fileB.slice(), 'chara')};
  if (sort === 3) {fileA = sortNames(fileB.slice(), 'chara').reverse()};
  if (sort === 4) {fileA = sortNames(fileB.slice(), 'state')};
  if (sort === 5) {fileA = sortNames(fileB.slice(), 'state').reverse()};
  return fileA;
}

// 判断是否本地图片
function ifLocalPic(url) {
  if (url.startsWith('http')) {
    const coverUrl = url;
    return coverUrl;
  } else if (url.startsWith('![[')) {
    let picnew5 = '';
    if (url.includes('/')) {
      const picnew2 = url.match(/(?<=\!\[\[).+(?:\/)(.+)(?=\]\])/);
      picnew5 = picfolder + picnew2[1];
    } else {
      const picnew2 = url.match(/(?<=\!\[\[).+(?=\]\])/g);
      picnew5 = picfolder + picnew2[0];
    }
    const coverUrl2 = app.vault.adapter.getResourcePath(picnew5);
    return coverUrl2;
  } else if (url.startsWith('![](')) {
    let picnew4 = '';
    if (url.includes('/')) {
      const picnew3 = url.match(/(?<=\!\[\]\().+(?:\/)(.+)(?=\))/);
      picnew4 = picfolder + picnew3[1].replace(/%20/g, ' ');
    } else {
      const picnew3 = url.match(/(?<=\!\[\]\().+(?=\))/g);
      picnew4 = picfolder + picnew3[0].replace(/%20/g, ' ');
    }
    const coverUrl3 = app.vault.adapter.getResourcePath(picnew4);
    return coverUrl3;
  } else {
    return yulanurl;
  }
}

function ifLocalPicWord(url) {
  if (url.startsWith('http')) {
    const coverUrl = ' ![face](' + url + ')';
    return coverUrl;
  } else if (url.startsWith('![[')) {
    let picnew5 = '';
    if (url.includes('/')) {
      const picnew2 = url.match(/(?<=\!\[\[).+(?:\/)(.+)(?=\]\])/);
      picnew5 = piclink + picnew2[1];
    } else {
      const picnew2 = url.match(/(?<=\!\[\[).+(?=\]\])/g);
      picnew5 = piclink + picnew2[0];
    }
    const coverUrl2 = ' ![[' + picnew5 + '|face]]';
    return coverUrl2;
  } else if (url.startsWith('![](')) {
    let picnew4 = '';
    if (url.includes('/')) {
      const picnew3 = url.match(/(?<=\!\[\]\().+(?:\/)(.+)(?=\))/);
      picnew4 = piclink.replace(/\s/g, '%20') + picnew3[1];
    } else {
      const picnew3 = url.match(/(?<=\!\[\]\().+(?=\))/g);
      picnew4 = piclink.replace(/\s/g, '%20') + picnew3[0];
    }
    const coverUrl3 =  ' ![face](' + picnew4 + ')';
    return coverUrl3;
  } else {
    return '';
  }
}

// 组合
const charaAlldiv = document.createElement("div");
const daohangall = document.createElement("div");
daohangall.classList.add('my-chat-sele');
daohangall.appendChild(daohangbut(selepage, selepageTitle, allnum, 'my-chat-selett'));
charaAlldiv.append(daohangall, seleshow, seleall);
seleall.append(sortData, listData, selename, selenull, seleExtraNull);

const charaContainer = document.createElement("div");
charaContainer.classList.add('chat-charafacebox');
const chatWordDiv = document.createElement("div");
function fy() { charaContainer.innerHTML = "";
  pagenum();
  files = sort1(tempfiles);
  if (favid.length !== 0) {
    let favnum = 0;
    for (var i=0; i < files.length; i++) {
      if (files[i].fav === true) {files[i].fav = false}
      for (var j=0; j < favid.length; j++) {
        if (files[i].id === favid[j]) {
          files[i].fav = true;
          const item1 = files[i];
          files.splice(i, 1);
          files.splice(favnum, 0, item1);
          favnum += 1;
        }
      }
    }
  } else {
    for (var i=0; i < files.length; i++) {
      if (files[i].fav === true) {files[i].fav = false}
    }
  }
  const num1 = global*listnum;
  const num2 = (global+1)*listnum;
  const num3 = files.length;
  const num4 = Math.min(num2, num3);
  for (var i = num1; i < num4; i++) {
    const idnum = files[i].id;
    const facediv = document.createElement("div");
    facediv.classList.add('chat-facediv');
    const cover = document.createElement('img');
    cover.classList.add('chat-facediv-img');
    const picold = files[i].link;
    const coverUrl = ifLocalPic(picold);
    cover.src = coverUrl;
    const timeoutId = setTimeout(() => {
      cover.src = errorurl;
    }, 5000);
    cover.onload = function() {
      clearTimeout(timeoutId);
    };
    cover.onerror = function() {
      clearTimeout(timeoutId);
      this.src = errorurl; // 更换src以显示默认图片
      this.onerror = null; // 防止无限循环
    };
    const chara1 = files[i].chara;
    const state1 = files[i].state;
    const charaname1 = chara1 + '(' + state1 + ')';
    if (charanum.length >= 1) {
      charanum.forEach(value => {
        if (value.id === idnum) {
          facediv.classList.add('chat-facediv-hover')
        }
      });
    }
    function coverClick() {
      if (facenum.length >= 1 || !empty(facenum2)) {
        if (facenum.length >= 1) {
          const facetemp = facenum.slice();
          facenum.forEach(p => {
            textlog[p].url = picold;
            textlog[p].name = chara1;
          });
          facenum = [];
          facetemp.forEach(p => {
            editframeOne(p, p);
          });
          styleword();
          codeRefresh();
          fy();
        }
        if (!empty(facenum2) && !facediv.classList.contains('chat-facediv-hover')) {
          const idindex6 = charanum.findIndex(item => item.id === facenum2);
          charanum[idindex6].id = idnum;
          localStorage.setItem('chatCharanum', JSON.stringify(charanum));
          facenum2 = null;
          createChatOne(idindex6, idindex6);
          fy();
        }
      } else {
        if (!facediv.classList.contains('chat-facediv-hover')) {
          chatWordDiv.appendChild(createChatChara(chara1, state1, picold, idnum, 0));
          let objtemp = {};
          objtemp.id = idnum;
          objtemp.li = 0;
          charanum.push(objtemp);
          localStorage.setItem('chatCharanum', JSON.stringify(charanum));
          facediv.classList.add('chat-facediv-hover');
          facetouch.ariaLabel = '';
        }
      }
    }
    facediv.appendChild(cover);
    const namediv = document.createElement("div");
    namediv.textContent = charaname1;
    namediv.classList.add('chat-namediv');
    facediv.appendChild(namediv);
    const facetouch = document.createElement("div");
    facetouch.classList.add('chat-facetouch');
    facetouch.onclick = ()=> {coverClick()}
    facediv.appendChild(facetouch);
    if (facenum.length >= 1) {
      facetouch.ariaLabel = t('t.tip2');
    } else if (!empty(facenum2) && !facediv.classList.contains('chat-facediv-hover')) {
      facetouch.ariaLabel = t('t.tip2');
    } else {
      if (!facediv.classList.contains('chat-facediv-hover')) {
        facetouch.ariaLabel = t('t.tip3');
      }
    }
    const favdiv = document.createElement("div");
    favdiv.textContent = " ";
    favdiv.classList.add('chat-favdiv');
    favdiv.ariaLabel = t('t.tip4');
    if (files[i].fav === true) {
      favdiv.classList.add('chat-favcards');
      favdiv.ariaLabel = t('t.tip5');
    }
    const favindex = i;
    favdiv.onclick = ()=> {
      if (files[favindex].fav === true) {
        files[favindex].fav = false;
        const numfav = favid.indexOf(files[favindex].id);
        favid.splice(numfav, 1);
        localStorage.setItem('chatFavid', JSON.stringify(favid));
        fy();
      } else {
        favid.push(files[favindex].id);
        localStorage.setItem('chatFavid', JSON.stringify(favid));
        fy();
      }
    }
    facediv.appendChild(favdiv);
    if (facenum.length >= 1 || (!empty(facenum2) && !facediv.classList.contains('chat-facediv-hover'))) {
      const replacediv = document.createElement("div");
      replacediv.innerHTML = replaceicon;
      replacediv.classList.add('chat-replacediv');
      facediv.appendChild(replacediv);
    }
    charaContainer.appendChild(facediv);
  }
};
charaAlldiv.appendChild(charaContainer);
charaAlldiv.appendChild(daohangbut(selepage2, selepageTitle2, allnum2, 'my-chat-sele2'));
inputSearch.addEventListener('keydown', function(event) {
  if (event.key === 'Enter' || event.code === 'Enter') {
    searchfile();
  }
});

// 显示隐藏选项
const showcheckdiv = document.createElement("div");
showcheckdiv.classList.add('chat-menubar');
const options4 = [t('t.name1'), t('t.name5'), t('t.name6'), t('t.name7'), t('t.name8')];
options4.forEach(function(option, index) {
  const checkbox = createCheckbox('showcheckbox' + index, option, option);
  const label = createLabel('showcheckbox' + index, option);
  if (showchecknum[index] === 0) {
    checkbox.checked = true;
  }
  if (index === 4) {
    label.classList.add('chat-label3');
    label.ariaLabel = t('t.tip6');
    checkbox.ariaLabel = t('t.tip6');
  } else {
    label.classList.add('chat-label2');
    label.ariaLabel = t('t.tip7') + option;
    checkbox.ariaLabel = t('t.tip7') + option;
  }
  showcheckdiv.append(checkbox, label);
});

const styleselediv = document.createElement("div");
if (showchecknum[0] === 0) {
  styleselediv.append(radioContainer, checkdiv, radio2Container);
};
const folderselediv = document.createElement("div");
if (showchecknum[1] === 0) {
  folderselediv.append(folderContainer1, folderContainer2, folderContainer3, folderContainer4);
}
const charaselediv = document.createElement("div");
if (showchecknum[2] === 0) {
  charaselediv.appendChild(charaAlldiv);
}
const charachatdiv = document.createElement("div");
const asideDiv = document.createElement("div");
asideDiv.style.marginBottom = '1rem';
asideDiv.appendChild(createChatChara(t('t.name9'), '', t('t.tag31'), 'aside1', 0));
if (showchecknum[3] === 0) {
  charachatdiv.append(chatWordDiv, asideDiv);
}

// 监听对话生成框的拖拽
chatWordDiv.addEventListener('dragstart', function(e) {
  if (e.target.classList.contains('chat-charaDiv')) {
    draggedItem = e.target;
    e.dataTransfer.effectAllowed = 'move';
    setTimeout(() => {
        draggedItem.style.opacity = '0.5';
    }, 0);
  }
});
chatWordDiv.addEventListener('dragover', function(e) {
  if (e.target.classList.contains('chat-charaDiv') && e.target !== draggedItem && draggedItem !== null) {
    e.preventDefault();
  }
});
chatWordDiv.addEventListener('dragenter', function(e) {
  if (e.target.classList.contains('chat-charaDiv') && e.target !== draggedItem && draggedItem !== null) {
    if (!e.target.classList.contains('chat-chara-before')) {
      e.target.classList.add('chat-chara-before');
    }
  }
});
chatWordDiv.addEventListener('dragleave', function(e) {
  if (e.target.classList.contains('chat-charaDiv') && e.target !== draggedItem && draggedItem !== null) {
    if (e.target.classList.contains('chat-chara-before')) {
      e.target.classList.remove('chat-chara-before');
    }
  }
});
chatWordDiv.addEventListener('drop', function(e) {
  if (e.target.classList.contains('chat-charaDiv') && e.target !== draggedItem && draggedItem !== null) {
    if (e.target.classList.contains('chat-chara-before')) {
      e.target.classList.remove('chat-chara-before');
    }
    const afterElement = e.target;
    const dragnum = Array.from(chatWordDiv.children).indexOf(draggedItem);
    const targetnum = Array.from(chatWordDiv.children).indexOf(afterElement);
    if (dragnum >= 0) {
      const obj0 = charanum[dragnum];
      if (dragnum > targetnum) {
        chatWordDiv.insertBefore(draggedItem, afterElement);
      } else {
        insertAfter(draggedItem, afterElement);
      }
      charanum.splice(dragnum,1);
      charanum.splice(targetnum,0,obj0);
      localStorage.setItem('chatCharanum', JSON.stringify(charanum));
    }
  }
});
chatWordDiv.addEventListener('dragend', function(e) {
  if (draggedItem) {
      draggedItem.style.opacity = '1';
      draggedItem.draggable = false;
  }
  draggedItem = null;
});

// 显示相关
showcheckdiv.addEventListener('change', function(event) {
  if (event.target.type === 'checkbox') {
    if (event.target.checked) {
      if (event.target.id === 'showcheckbox0') {
        styleselediv.append(radioContainer, checkdiv, radio2Container);
        showchecknum[0] = 0;
        localStorage.setItem('chatShowchecknum', JSON.stringify(showchecknum));
        setCode();
      }
      if (event.target.id === 'showcheckbox1') {
        folderselediv.append(folderContainer1, folderContainer2, folderContainer3, folderContainer4);
        showchecknum[1] = 0;
        localStorage.setItem('chatShowchecknum', JSON.stringify(showchecknum));
      }
      if (event.target.id === 'showcheckbox2') {
        charaselediv.appendChild(charaAlldiv);
        showchecknum[2] = 0;
        localStorage.setItem('chatShowchecknum', JSON.stringify(showchecknum));
        fy();
      }
      if (event.target.id === 'showcheckbox3') {
        createChat();
        charachatdiv.append(chatWordDiv, asideDiv);
        showchecknum[3] = 0;
        localStorage.setItem('chatShowchecknum', JSON.stringify(showchecknum));
      }
      if (event.target.id === 'showcheckbox4') {
        piclink = '';styleword();
        codeRefresh();
        showchecknum[4] = 0;
        localStorage.setItem('chatShowchecknum', JSON.stringify(showchecknum));
      }
    } else {
      if (event.target.id === 'showcheckbox0') {
        styleselediv.innerHTML = "";
        showchecknum[0] = 1;
        localStorage.setItem('chatShowchecknum', JSON.stringify(showchecknum));
      }
      if (event.target.id === 'showcheckbox1') {
        folderselediv.innerHTML = "";
        showchecknum[1] = 1;
        localStorage.setItem('chatShowchecknum', JSON.stringify(showchecknum));
      }
      if (event.target.id === 'showcheckbox2') {
        charaselediv.innerHTML = "";
        showchecknum[2] = 1;
        localStorage.setItem('chatShowchecknum', JSON.stringify(showchecknum));
      }
      if (event.target.id === 'showcheckbox3') {
        charachatdiv.innerHTML = "";
        facenum2 = null;
        if (showchecknum[2] === 0) {fy()};
        showchecknum[3] = 1;
        localStorage.setItem('chatShowchecknum', JSON.stringify(showchecknum));
      }
      if (event.target.id === 'showcheckbox4') {
        piclink = picfolder;
        showchecknum[4] = 1;
        localStorage.setItem('chatShowchecknum', JSON.stringify(showchecknum));
        styleword();
        codeRefresh();
      }
    }
  }
});

// 编辑文字
function textinput(div, str) {
  const inputtext = div.value;
  const startPos = div.selectionStart;
  const endPos = div.selectionEnd;
  const copytext = inputtext.substring(startPos, endPos);
  let edittext = '';
  if (str !== '\n') {
    if (checknum[8] === 0) {
      edittext = str + copytext + str;
    } else {
      switch (str) {
        case '**':
          edittext = '<b>' + copytext + '</b>';
          break;
        case '*':
          edittext = '<em>' + copytext + '</em>';
          break;
        case '==':
          edittext = '<mark>' + copytext + '</mark>';
          break;
        case '~~':
          edittext = '<del>' + copytext + '</del>';
          break;
        default:
          edittext = copytext;
      }
    }
  } else {
    edittext = copytext + '\n';
  }
  const beforeSelection = inputtext.substring(0, startPos);
  const afterSelection = inputtext.substring(endPos, inputtext.length);
  div.value = beforeSelection + edittext + afterSelection;
  div.selectionStart = div.selectionEnd = startPos + edittext.length;
  div.style.height = 'auto';
  div.style.height = (div.scrollHeight) + 'px';
  div.focus();
}

function creditbut(icon, label, div, str) {
  const editbut = document.createElement("span");
  editbut.innerHTML = obsiIcon2(icon, 16);
  editbut.ariaLabel = label;
  editbut.classList.add('chat-namebutton');
  editbut.onclick = ()=> {textinput(div, str)}
  return editbut
}

// 对话生成框
function createChatChara(name, state, url, id, li) {
  const charaDiv = document.createElement("div");
  charaDiv.classList.add('chat-charaDiv');
  const cover = document.createElement('img');
  cover.classList.add('chat-chara-img');
  const picold = url;
  const coverUrl = ifLocalPic(picold);
  cover.src = coverUrl;
  const timeoutId = setTimeout(() => {
    cover.src = errorurl;
  }, 5000);
  cover.onload = function() {
    clearTimeout(timeoutId);
  };
  cover.onerror = function() {
    clearTimeout(timeoutId);
    this.src = errorurl;
    this.onerror = null;
  };
  const coverdiv = document.createElement("div");
  coverdiv.classList.add('chat-coverdiv');
  const coverselediv = document.createElement("div");
  coverselediv.id = 'coversele' + id;
  coverselediv.innerHTML = replaceicon;
  coverselediv.ariaLabel = t('t.tip8');
  coverselediv.classList.add('chat-coverselediv');
  coverselediv.onclick = ()=> {
    if (!coverselediv.classList.contains('chat-coverselediv-on')) {
      if (!empty(facenum2)) {
        const otherdiv = document.getElementById(`coversele${facenum2}`);
        if (otherdiv) {
          otherdiv.classList.remove('chat-coverselediv-on');
        }
      }
      coverselediv.classList.add('chat-coverselediv-on');
      facenum2 = id;
      if (showchecknum[2] === 0) {fy()};
    } else {
      coverselediv.classList.remove('chat-coverselediv-on');
      facenum2 = null;
      if (showchecknum[2] === 0) {fy()};
    }
  }
  if (!empty(facenum2)) {
    if (facenum2 === id) {
      coverselediv.classList.add('chat-coverselediv-on');
    }
  }
  coverdiv.append(cover, coverselediv);

  const charaeditDiv = document.createElement("div");
  charaeditDiv.classList.add('chat-chara2Div');
  const rowDiv1 = document.createElement("div");
  rowDiv1.innerHTML = upicon;
  rowDiv1.ariaLabel = t('t.tip9');
  rowDiv1.classList.add('chat-row-button');
  rowDiv1.onclick = ()=> {
    const index2 = charanum.findIndex(item => item.id === id);
    let indexnew = 0;
    const obj0 = charanum[index2];
    if (index2 === 0) {
      charanum.splice(0,1);
      charanum.push(obj0);
      indexnew = charanum.length - 1;
    } else {
      charanum.splice(index2,1);
      charanum.splice(index2 - 1,0,obj0);
      indexnew = index2 - 1;
    };
    localStorage.setItem('chatCharanum', JSON.stringify(charanum));
    createChatOne(index2, indexnew);
  }
  const rowDiv2 = document.createElement("div");
  rowDiv2.innerHTML = downicon;
  rowDiv2.ariaLabel = t('t.tip10');
  rowDiv2.classList.add('chat-row-button');
  rowDiv2.onclick = ()=> {
    const index2 = charanum.findIndex(item => item.id === id);
    let indexnew = 0;
    const obj0 = charanum[index2];
    if (index2 === charanum.length - 1) {
      charanum.splice(index2,1);
      charanum.unshift(obj0);
    } else {
      charanum.splice(index2,1);
      charanum.splice(index2 + 1,0,obj0);
      indexnew = index2 + 1;
    };
    localStorage.setItem('chatCharanum', JSON.stringify(charanum));
    createChatOne(index2, indexnew);
  }

  const clearbut = document.createElement("span");
  clearbut.innerHTML = '✕';
  clearbut.ariaLabel = t('t.tip11');
  clearbut.classList.add('chat-clear-button');
  clearbut.onclick = ()=> {
    surebox.style.display = 'flex';
    sureResult = 1;
    idtemp = charanum.findIndex(item => item.id === id);
  }
  const clearbutAll = document.createElement("span");
  clearbutAll.innerHTML = deleteicon;
  clearbutAll.ariaLabel = t('t.tip12');
  clearbutAll.classList.add('chat-clear-button2');
  clearbutAll.onclick = ()=> {
    surebox.style.display = 'flex';
    sureResult = 4;
  }

  const movediv = document.createElement("div");
  movediv.innerHTML = gripicon;
  movediv.ariaLabel = t('t.tip13');
  movediv.classList.add('chat-moveDiv');
  movediv.addEventListener('mouseenter', function() {
    charaDiv.draggable = true;
  });
  movediv.addEventListener('mouseleave', function() {
    charaDiv.draggable = false;
  });
  movediv.addEventListener('touchstart', function() {
    charaDiv.draggable = true;
  });
  movediv.addEventListener('touchend', function() {
    charaDiv.draggable = false;
  });

  let wordname = '';
  if (id !== 'aside1') {wordname = name + '(' + state + ')';
  } else {wordname = name}
  const worddiv = document.createElement("div");
  worddiv.classList.add('chat-worddiv');
  const namebutdivall = document.createElement("div");
  namebutdivall.classList.add('chat-namebutall');
  const namebutdiv = document.createElement("div");
  namebutdiv.classList.add('chat-namebut');
  namebutdivall.appendChild(namebutdiv);
  const namediv2 = document.createElement("div");
  namediv2.textContent = wordname;
  namediv2.classList.add('chat-chara-namediv2');
  namebutdiv.appendChild(namediv2);
  const rightcheckbox = createCheckbox('rightcheckbox' + id, t('t.tip14'), t('t.tip14'));
  const rightchecklabel = createLabel('rightcheckbox' + id, t('t.tip14'));
  if (li === 1) {rightcheckbox.checked = true};
  rightchecklabel.classList.add('chat-label2');
  if (id !== 'aside1') {
    namediv2.append(rightcheckbox, rightchecklabel);
  }

  let typenum = 0;
  let wordlistnum = 0;

  const seletypeTitle = document.createElement("div");
  const seletypeUl = document.createElement("section");
  const seletype = seleBut(seletypeTitle, seletypeUl, 'chat-menubut-up', 'chat-sele-titlexj', t('t.tip15'));
  seletypeTitle.textContent = t('t.tip16');

  function typebut(nadiv, inner, numdiv) {
    nadiv = document.createElement("div");
    nadiv.classList.add('my-seleop-chat');
    nadiv.textContent = inner;
    nadiv.onclick = ()=> {
      typenum = numdiv;seletypeTitle.textContent = inner;
      relist();
    }
    return nadiv;
  }
  seletypeUl.appendChild(typebut('type1', t('t.tip16'), 0));
  seletypeUl.appendChild(typebut('type2', t('t.tip17'), 1));

  const selelistTitle = document.createElement("div");
  const selelistUl = document.createElement("section");
  const selelist = seleBut(selelistTitle, selelistUl, 'chat-menubut-up', 'chat-sele-titlexj', t('t.tip18'));
  selelistTitle.addEventListener('mouseenter', () => {relist()});

  // 重置行数选择按钮
  function relist() {
    selelistUl.innerHTML = "";
    wordlistnum = 0;
    if (typenum === 0) {selelistTitle.textContent = t('t.tip19');
    } else {selelistTitle.textContent = t('t.tag31');}
    const selelistNoneop = document.createElement("div");
    selelistNoneop.classList.add('my-seleop-chat');
    let numtext2 = '';
    if (typenum === 0) {numtext2 = t('t.tip19');
    } else {numtext2 = t('t.tag31')}
    selelistNoneop.textContent = numtext2;
    selelistNoneop.onclick = ()=> {
          selelistTitle.textContent = numtext2;
          wordlistnum = 0;
    }
    selelistUl.appendChild(selelistNoneop);

    if (textlog[0]) {
      for (let i = 0; i < textlog.length; i++) {
        let selelistop = document.createElement("div");
        selelistop.classList.add('my-seleop-chat');
        const tempnum = i + 1;
        const numtext = fix(tempnum, 3);
        selelistop.textContent = numtext;
        selelistop.onclick = ()=> {
          selelistTitle.textContent = numtext;
          wordlistnum = tempnum;
        }
        selelistUl.appendChild(selelistop);
      }
    }
  };relist();

  const textareaWord = document.createElement("textarea");
  textareaWord.rows = "3";
  textareaWord.cols = "50";
  textareaWord.classList.add('chat-textareaWord');
  textareaWord.addEventListener('keydown', function(event) {
    if (event.key === 'Enter' || event.code === 'Enter') {
      if ((!event.shiftKey)) {
        event.preventDefault();
        inputword(this.value);
        this.value = '';
      }
      this.style.height = 'auto';
      this.style.height = (this.scrollHeight) + 'px';
    }
  });
  function inputword(text) {
    if (empty(text)) {
      new obsidian.Notice(t('t.notice8'), 3000);
    } else {
      let charaobj = {};
      if (id !== 'aside1') {
        if (rightcheckbox.checked) {
          charaobj.symbol = '+';
        } else {
          charaobj.symbol = '-';
        }
      } else {
        charaobj.symbol = 'p';
      }
      charaobj.url = url;
      charaobj.name = name;
      charaobj.word = text;
      if (wordlistnum !== 0 && wordlistnum > textlog.length) {
        wordlistnum = textlog.length;
      }
      if (wordlistnum !== 0) {
        if (typenum === 0) {
          textlog.splice(wordlistnum - 1,0,charaobj);
        } else if (typenum === 1) {
          textlog.splice(wordlistnum - 1,1,charaobj);
        }
      } else {textlog.push(charaobj)}
      if (showchecknum2[0] === 1) {
        const textlog2 = textlog.slice();
        let textindex = 0;
        if (wordlistnum !== 0) {
          textindex = wordlistnum - 1;
          if (typenum === 0) {
            editframeOneAdd(textindex);
            changelistnum();
          } else if (typenum === 1) {
            editframeOne(textindex, textindex);
          }
        } else {
          textindex = textlog2.length - 1;
          editframeOneAdd(textindex);
        }
      };
      styleword();
      relist();
      codeRefresh();
    }
  }

  textareaWord.addEventListener('input', function() {
    this.style.height = 'auto';
    this.style.height = (this.scrollHeight) + 'px';
  });

  const boldbut = creditbut('lucide-bold', t('t.tip20'), textareaWord, '**');
  const italicbut = creditbut('lucide-italic', t('t.tip21'), textareaWord, '*')
  const highlightbut = creditbut('lucide-highlighter', t('t.tip22'), textareaWord, '==')
  const strikethroughbut = creditbut('lucide-strikethrough', t('t.tip23'), textareaWord, '~~')
  const arrowbut = creditbut('lucide-corner-down-left', t('t.tip24'), textareaWord, '\n')

  const wordbut = document.createElement("span");
  wordbut.innerHTML = penicon;
  wordbut.ariaLabel = t('t.Input');
  wordbut.classList.add('chat-edit-button');
  wordbut.onclick = ()=> {
    inputword(textareaWord.value);
    textareaWord.value = '';
    textareaWord.style.height = 'auto';
    textareaWord.style.height = (textareaWord.scrollHeight) + 'px';
  }
  const namebutdiv2 = document.createElement("div");
  namebutdiv2.classList.add('chat-namebutdiv2');
  const namebutdiv3 = document.createElement("div");
  namebutdiv3.classList.add('chat-namebutdiv3');
  const bottomdiv = document.createElement('div');
  bottomdiv.classList.add('chat-bottomdiv');
  namebutdiv.append(boldbut, italicbut, highlightbut, strikethroughbut, arrowbut, namebutdiv2);
  namebutdiv2.append(seletype, selelist);

  if (id !== 'aside1') {
    namebutdivall.append(movediv, namebutdiv3);
    namebutdiv3.append(rowDiv1, rowDiv2, clearbut);
  } else {
    namebutdiv2.appendChild(clearbutAll);
  };
  worddiv.appendChild(textareaWord);
  bottomdiv.append(charaeditDiv, wordbut);
  charaDiv.append(namebutdivall, bottomdiv);

  rightcheckbox.addEventListener('change', function() {
    charaeditDiv.innerHTML = "";
    if (this.checked) {
      charaeditDiv.append(worddiv, coverdiv);
      const idindex4 = charanum.findIndex(item => item.id === id);
      charanum[idindex4].li = 1;
      localStorage.setItem('chatCharanum', JSON.stringify(charanum));
    } else {
      charaeditDiv.append(coverdiv, worddiv);
      const idindex5 = charanum.findIndex(item => item.id === id);
      charanum[idindex5].li = 0;
      localStorage.setItem('chatCharanum', JSON.stringify(charanum));
    }
  });
  if (id === 'aside1') {charaeditDiv.appendChild(worddiv);
  } else if (li === 1) {
    charaeditDiv.append(worddiv, coverdiv);
  } else {
    charaeditDiv.append(coverdiv, worddiv);
  }
  return charaDiv;
}

// 生成本地数据对话框
function createChat() {
  chatWordDiv.innerHTML = "";
  facenum2 = null;
  if (showchecknum[2] === 0) {fy()};
  if (charanum.length !== 0) {
    charanum.forEach(value => {
      const indexAll = allfiles.findIndex(item => item.id === value.id);
      const picold2 = allfiles[indexAll].link;
      const chara2 = allfiles[indexAll].chara;
      const state2 = allfiles[indexAll].state;
      const word5 = value.id;
      const li1 = value.li;
      chatWordDiv.appendChild(createChatChara(chara2, state2, picold2, word5, li1));
    });
  }
}
if (showchecknum[3] === 0) {createChat()}

function createChatOne(oldnum, newnum) {
  chatWordDiv.removeChild(chatWordDiv.children[oldnum]);
  const value = charanum[newnum];
  const indexAll = allfiles.findIndex(item => item.id === value.id);
  const picold2 = allfiles[indexAll].link;
  const chara2 = allfiles[indexAll].chara;
  const state2 = allfiles[indexAll].state;
  const word5 = value.id;
  const li1 = value.li;
  const newElement = createChatChara(chara2, state2, picold2, word5, li1);
  const children = chatWordDiv.children;
  if (newnum < children.length) {
    chatWordDiv.insertBefore(newElement, children[newnum]);
  } else {
    chatWordDiv.appendChild(newElement);
  }
}

// 编辑框
const editdiv = document.createElement("div");

editdiv.addEventListener('dragstart', function(e) {
  if (e.target.classList.contains('chat-editDiv')) {
    draggedItem2 = e.target;
    e.dataTransfer.effectAllowed = 'move';
    setTimeout(() => {
        draggedItem2.style.opacity = '0.5';
    }, 0);
  }
});
editdiv.addEventListener('dragover', function(e) {
  if (e.target.classList.contains('chat-editDiv') && e.target !== draggedItem2 && draggedItem2 !== null) {
    e.preventDefault();
  }
});
editdiv.addEventListener('dragenter', function(e) {
  if (e.target.classList.contains('chat-editDiv') && e.target !== draggedItem2 && draggedItem2 !== null) {
    if (!e.target.classList.contains('chat-chara-before')) {
      e.target.classList.add('chat-chara-before');
    }
  }
});
editdiv.addEventListener('dragleave', function(e) {
  if (e.target.classList.contains('chat-editDiv') && e.target !== draggedItem2 && draggedItem2 !== null) {
    if (e.target.classList.contains('chat-chara-before')) {
      e.target.classList.remove('chat-chara-before');
    }
  }
});
editdiv.addEventListener('drop', function(e) {
  if (e.target.classList.contains('chat-editDiv') && e.target !== draggedItem2 && draggedItem2 !== null) {
    if (e.target.classList.contains('chat-chara-before')) {
      e.target.classList.remove('chat-chara-before');
    }
    const afterElement = e.target;
    const dragnum = Array.from(editdiv.children).indexOf(draggedItem2);
    const targetnum = Array.from(editdiv.children).indexOf(afterElement);
    if (dragnum >= 0) {
      const obj1 = textlog[dragnum];
      textlog.splice(dragnum,1);
      textlog.splice(targetnum,0,obj1);
      editframeOne(dragnum, targetnum);
      changelistnum();
      styleword();
      codeRefresh();
    }
  }
});
editdiv.addEventListener('dragend', function(e) {
  if (draggedItem2) {
      draggedItem2.style.opacity = '1';
  }
  draggedItem2 = null;
});

function editOne(value, indexnum) {
  const charaADiv = document.createElement("div");
  charaADiv.classList.add('chat-editDiv');
  const charaeditDiv = document.createElement("div");
  charaeditDiv.classList.add('chat-chara2Div2');

  const rowDiv1 = document.createElement("div");
  rowDiv1.innerHTML = upicon;
  rowDiv1.ariaLabel = t('t.tip9');
  rowDiv1.classList.add('chat-row-button');
  rowDiv1.onclick = ()=> {
    const index = findnum(charaADiv);
    let indexnew = 0;
    if (index === 0) {
      textlog.splice(0,1);
      textlog.push(value);
      indexnew = textlog.length - 1;
    } else {
      textlog.splice(index,1);
      textlog.splice(index - 1,0,value);
      indexnew = index - 1;
    };
    editframeOne(index, indexnew);
    changelistnum();
    styleword();
    codeRefresh();
  }
  const rowDiv2 = document.createElement("div");
  rowDiv2.innerHTML = downicon;
  rowDiv2.ariaLabel = t('t.tip10');
  rowDiv2.classList.add('chat-row-button');
  rowDiv2.onclick = ()=> {
    const index = findnum(charaADiv);
    let indexnew = 0;
    if (index === textlog.length - 1) {
      textlog.splice(index,1);
      textlog.unshift(value);
    } else {
      textlog.splice(index,1);
      textlog.splice(index + 1,0,value);
      indexnew = index + 1;
    };
    editframeOne(index, indexnew);
    changelistnum();
    styleword();
    codeRefresh();
  }

  const clearbut = document.createElement("span");
  clearbut.innerHTML = '✕';
  clearbut.ariaLabel = t('t.tip25');
  clearbut.classList.add('chat-clear-button');
  clearbut.onclick = ()=> {
    const index = findnum(charaADiv);
    surebox.style.display = 'flex';
    sureResult = 2;
    indextemp = index;
  }

  const movediv = document.createElement("div");
  movediv.innerHTML = gripicon;
  movediv.ariaLabel = t('t.tip13');
  movediv.classList.add('chat-moveDiv');
  movediv.addEventListener('mouseenter', function() {
    charaADiv.draggable = true;
  });
  movediv.addEventListener('mouseleave', function() {
    charaADiv.draggable = false;
  });
  movediv.addEventListener('touchstart', function() {
    charaADiv.draggable = true;
  });
  movediv.addEventListener('touchend', function() {
    charaADiv.draggable = false;
  });

  const worddiv = document.createElement("div");
  worddiv.classList.add('chat-worddiv2');
  const namebutdivall = document.createElement("div");
  namebutdivall.classList.add('chat-namebutall');
  const namebutdiv = document.createElement("div");
  namebutdiv.classList.add('chat-namebut');
  namebutdivall.appendChild(namebutdiv);

  const textareaWord = document.createElement("textarea");
  const wordtext = value.word.split("\n");
  let wordflat = [];
  let text2 = '';
  for (var i=0; i < wordtext.length; i++) {
    if (!empty(wordtext[i])) {wordflat.push(wordtext[i])}
  }
  for (var i=0; i < wordflat.length; i++) {
    if (i === 0) {
      text2 += wordflat[i];
    } else {
      text2 += '\n' + wordflat[i];
    }
  }
  textareaWord.value = text2;
  textareaWord.rows = `${wordflat.length}`;
  textareaWord.cols = "50";
  textareaWord.classList.add('chat-textareaWord2');
  textareaWord.addEventListener('keydown', function(event) {
    if (event.key === 'Enter' || event.code === 'Enter') {
      if ((!event.shiftKey)) {
        event.preventDefault();
        inputword(this.value);
        this.blur();
      }
      this.style.height = 'auto';
      this.style.height = (this.scrollHeight) + 'px';
    }
  });
  textareaWord.addEventListener('blur', function() {
    inputword(this.value);
    this.style.height = 'auto';
    this.style.height = (this.scrollHeight) + 'px';
  });
  function inputword(text) {
    if (empty(text)) {
      new obsidian.Notice(t('t.notice8'), 3000);
    } else {
      const index = findnum(charaADiv);
      textlog[index].word = text;
      styleword();
      codeRefresh();
    }
  }

  textareaWord.addEventListener('input', function() {
    this.style.height = 'auto';
    this.style.height = (this.scrollHeight) + 'px';
  });
  const boldbut = creditbut('lucide-bold', t('t.tip20'), textareaWord, '**');
  const italicbut = creditbut('lucide-italic', t('t.tip21'), textareaWord, '*')
  const highlightbut = creditbut('lucide-highlighter', t('t.tip22'), textareaWord, '==')
  const strikethroughbut = creditbut('lucide-strikethrough', t('t.tip23'), textareaWord, '~~')
  const arrowbut = creditbut('lucide-corner-down-left', t('t.tip24'), textareaWord, '\n')
  const copybut = document.createElement("span");
  copybut.innerHTML = obsiIcon2('lucide-copy-plus', 16);
  copybut.ariaLabel = t('t.tip26');
  copybut.classList.add('chat-namebutton2');
  copybut.onclick = ()=> {
    let charaobj = {};
    if (value.symbol === 'p') {
      charaobj.symbol = 'p';
    } else {
      charaobj.symbol = value.symbol;
      charaobj.url = value.url;
      charaobj.name = value.name;
    };
    charaobj.word = value.word;
    const index = findnum(charaADiv);
    textlog.splice(index + 1,0,charaobj);
    editframeOneAdd(index + 1);
    changelistnum();
    styleword();
    codeRefresh();
  }
  const wordbut = document.createElement("span");
  wordbut.innerHTML = penicon;
  wordbut.ariaLabel = t('t.Input');
  wordbut.classList.add('chat-edit-button');
  wordbut.onclick = ()=> {
    inputword(textareaWord.value);
    textareaWord.style.height = 'auto';
    textareaWord.style.height = (textareaWord.scrollHeight) + 'px';
  }
  const listshow = document.createElement("span");
  listshow.textContent = fix(indexnum + 1, 3);
  listshow.classList.add('chat-listshow');
  const namediv2 = document.createElement("div");
  namediv2.classList.add('chat-chara-namediv2');
  const namebutdiv3 = document.createElement("div");
  namebutdiv3.classList.add('chat-namebutdiv3');
  namebutdiv3.append(rowDiv1, rowDiv2, clearbut);
  worddiv.append(namebutdivall, textareaWord);
  charaADiv.append(charaeditDiv, listshow, wordbut);

  if (value.symbol === 'p') {
    namediv2.textContent = t('t.name9');
    namebutdiv.append(namediv2, boldbut, italicbut, highlightbut, strikethroughbut, arrowbut, copybut);
    namebutdivall.append(movediv, namebutdiv3);
    charaeditDiv.appendChild(worddiv);
  } else {
    const cover = document.createElement('img');
    cover.classList.add('chat-chara-img');
    const picold = value.url;
    const coverUrl = ifLocalPic(picold);
    cover.src = coverUrl;
    const timeoutId = setTimeout(() => {
      cover.src = errorurl;
    }, 5000);
    cover.onload = function() {
      clearTimeout(timeoutId);
    };
    cover.onerror = function() {
      clearTimeout(timeoutId);
      this.src = errorurl;
      this.onerror = null;
    };
    const coverdiv = document.createElement("div");
    coverdiv.classList.add('chat-coverdiv');
    const coverselediv = document.createElement("div");
    coverselediv.innerHTML = replaceicon;
    coverselediv.ariaLabel = t('t.tip8');
    coverselediv.classList.add('chat-coverselediv');
    let coverchange = 0;
    coverselediv.onclick = ()=> {
      const index = findnum(charaADiv);
      if (coverchange === 0) {
        coverchange = 1;
        coverselediv.classList.add('chat-coverselediv-on');
        facenum.push(index);
        if (showchecknum[2] === 0) {fy()};
      } else {
        coverchange = 0;
        coverselediv.classList.remove('chat-coverselediv-on');
        const delenum = facenum.indexOf(index);
        facenum.splice(delenum,1);
        if (showchecknum[2] === 0) {fy()};
      }
    }
    if (facenum.length >= 1) {
      if (facenum.includes(indexnum)) {
        coverchange = 1;
        coverselediv.classList.add('chat-coverselediv-on');
      }
    }
    coverdiv.append(cover, coverselediv);
    namediv2.textContent = value.name;
    namebutdiv.appendChild(namediv2);
    const id3 = indexnum;
    const rightcheckbox = createCheckbox('rightcheckbox-edit' + id3, t('t.tip14'), t('t.tip14'));
    const rightchecklabel = createLabel('rightcheckbox-edit' + id3, t('t.tip14'));
    rightchecklabel.classList.add('chat-label2');
    namediv2.append(rightcheckbox, rightchecklabel);
    namebutdiv.append(boldbut, italicbut, highlightbut, strikethroughbut, arrowbut, copybut);
    namebutdivall.append(movediv, namebutdiv3);

    rightcheckbox.addEventListener('change', function() {
      charaeditDiv.innerHTML = "";
      const index = findnum(charaADiv);
      if (this.checked) {
        charaeditDiv.append(worddiv, coverdiv);
        textlog[index].symbol = '+';
        styleword();
        codeRefresh();
      } else {
        charaeditDiv.append(coverdiv, worddiv);
        textlog[index].symbol = '-';
        styleword();
        codeRefresh();
      }
    });
    if (value.symbol === '-') {
      charaeditDiv.append(coverdiv, worddiv);
    } else {
      rightcheckbox.checked = true;
      charaeditDiv.append(worddiv, coverdiv);
    }
  }
  return charaADiv;
}

function editframe() {
  editdiv.innerHTML = "";
  facenum = [];
  if (showchecknum[2] === 0) {fy()};
  const textlog2 = textlog.slice();
  if (textlog2[0]) {
    textlog2.map(function(value, index) {
      editdiv.appendChild(editOne(value, index));
    });
  }
}

function findnum(tempdiv) {
  const num = Array.from(editdiv.children).indexOf(tempdiv);
  return num;
}
// 替换模式
function editframeOne(oldnum, newnum) {
  editdiv.removeChild(editdiv.children[oldnum]);
  const textlog2 = textlog.slice();
  const value = textlog2[newnum];
  const ifface = facenum.includes(oldnum);
  if (facenum.length >= 1) {
    if (ifface) {
      const delenum = facenum.indexOf(oldnum);
      facenum.splice(delenum,1);
    }
    if (facenum.length >= 1) {
      facenum.forEach((p, index) => {
        if (p > oldnum) {
          facenum[index] = p - 1;
        }
      });
    }
    if (facenum.length >= 1) {
      facenum.forEach((p, index) => {
        if (newnum <= p) {
          facenum[index] = p + 1;
        }
      });
    }
    if (ifface) {facenum.push(newnum)}
  }
  const newElement = editOne(value, newnum);
  const children = editdiv.children;
  if (newnum < children.length) {
    editdiv.insertBefore(newElement, children[newnum]);
  } else {
    editdiv.appendChild(newElement);
  }
}
// 添加模式
function editframeOneAdd(num) {
  const textlog2 = textlog.slice();
  const value = textlog2[num];
  if (facenum.length >= 1) {
    facenum.forEach((p, index) => {
      if (num <= p) {
        facenum[index] = p + 1;
      }
    });
  }
  const newElement = editOne(value, num);
  const children = editdiv.children;
  if (num < children.length) {
    editdiv.insertBefore(newElement, children[num]);
  } else {
    editdiv.appendChild(newElement);
  }
}

// 修改编号
function changelistnum() {
  const listtemp = editdiv.querySelectorAll('.chat-listshow');
  if (listtemp) {
    listtemp.forEach((e, index) => {
      e.textContent = fix(index + 1, 3);
    });
  }
  const checktemp = editdiv.querySelectorAll('input[type="checkbox"]');
  const labeltemp = editdiv.querySelectorAll('label');
  if (checktemp) {
    checktemp.forEach((e, index) => {
      e.id = 'rightcheckbox-edit' + index;
      labeltemp[index].htmlFor = 'rightcheckbox-edit' + index;
    });
  }
}

// 代码框
const codeShow = document.createElement("div");
const codeEditDiv = document.createElement("div");
codeEditDiv.classList.add('chat-codeEditDiv');
const textareaCode = document.createElement("textarea");
textareaCode.rows = "10";
textareaCode.cols = "50";
textareaCode.classList.add('chat-textareaWord2');

textareaCode.addEventListener('keydown', function(event) {
  if (event.key === 'Enter' || event.code === 'Enter') {
    this.style.height = 'auto';
    this.style.height = (this.scrollHeight) + 'px';
  }
});

function inputcode(text) {
  if (empty(text)) {
    resetCode();
    styleword();
    if (showchecknum2[0] === 1) {editframe()};
    codeRefresh();
  } else {
    resetCode();
    const lines = text.split("\n");
    lines.forEach(function(value, index) {
      if (index === 0) {
        if (empty(value)) {
          titletext = '';
          inputTitle.value = '';
          checknum[0] = 1;
        } else {
          const textline = value.match(/[^\s]+/g);
          if (textline[1]) {
            if (value.startsWith('> [!chatbox')) {
              if (textline[1].includes('bbs')) {radionum = 1};
              if (textline[1].includes('pop')) {radionum = 2};
              if (textline[1].includes('wechat')) {radionum = 3};
              if (textline[1].includes('qqchat')) {radionum = 4};
              if (textline[1].includes('linshe')) {radionum = 5};
              if (textline[1].includes('baker')) {radionum = 6};
              if (textline[1].includes('notitle')) {checknum[0] = 1};
              if (textline[1].includes('fix')) {checknum[1] = 1};
              if (textline[1].includes('short')) {checknum[2] = 1};
              if (textline[1].includes('frame')) {checknum[3] = 1};
              if (textline[1].includes('noname')) {checknum[4] = 1};
              if (textline[1].includes('noface')) {checknum[5] = 1};
              if (textline[1].includes('long')) {checknum[6] = 1};
              if (textline[1].includes('point')) {checknum[7] = 1};
              if (textline[1].includes('htmltag')) {checknum[8] = 1};
              radionum2 = 0;
              if (textline[1].includes(']+')) {radionum2 = 1};
              if (textline[1].includes(']-')) {radionum2 = 2};
              if (textline.length >= 3) {
                const linetitle = value.match(/(?<=\]\s|\+\s|\-\s)(.+)/g);
                titletext = linetitle[0].trim();
                inputTitle.value = linetitle[0].trim();
              } else {
                titletext = '';
                inputTitle.value = '';
              }
            } else {
              titletext = value.trim();
              inputTitle.value = value.trim();
            }
          } else {
            titletext = value.trim();
            inputTitle.value = value.trim();
          }
        }
      } else {
        let textobj = {};
        if (empty(value)) {
          value = '';
        } else {
          value = value.trim();
        }
        if (!value.startsWith('> ')) {
          if (value.startsWith('>')) {
            const word6 = value.substring(1);
            value = '> ' + word6;
          } else {
            value = '> ' + value;
          }
        }
        if (!value.startsWith('> - ') && !value.startsWith('> + ')) {
          if (value.startsWith('> -')) {
            const word7 = value.substring(3);
            value = '> - ' + word7;
          }
          if (value.startsWith('> +')) {
            const word7 = value.substring(3);
            value = '> + ' + word7;
          }
          if (value !== '> ' && value !== '> <span></span>') {
            if (codechatON === true) {
              const word7 = value.substring(2);
              value = '> - ' + word7;
            }
          }
        }
        const textline2 = value.match(/[^\s]+/g);
        if (textline2.length === 2) {
          if (index !== 1 && lines[index - 1] !== '> ' && !empty(lines[index - 1])) {
            textobj.symbol = 'c';
            textobj.word = textline2[1];
            textlog.push(textobj);
          } else if (textline2[1] !== '<span></span>') {
            textobj.symbol = 'p';
            textobj.word = textline2[1];
            textlog.push(textobj);
          }
        } else if (textline2.length > 2) {
          function textnext() {
            if (textline2[2].startsWith('!')) {
              if (textline2[2].startsWith('![face](')) {
                const faceurl = textline2[2].match(/(?<=face\]\()(.*)(?=\))/g);
                if (faceurl[0].startsWith('http')) {
                  textobj.url = faceurl[0];
                } else {
                  textobj.url = '![](' + faceurl[0] + ')';
                }
                if (!empty(textline2[3])) {
                  if (textline2[3].startsWith('*')) {
                    textobj.name = textline2[3].replace(/\*/g, '');
                    const word3 = value.match(/(?<=\*\s)(.*)/g);
                    if (!empty(word3)) {textobj.word = word3[0].trim();
                    } else {textobj.word = ''}
                    textlog.push(textobj);
                  } else {
                    textobj.name = '';
                    const word3 = value.match(/(?<=\)\s)(.*)/g);
                    textobj.word = word3[0].trim();
                    textlog.push(textobj);
                  }
                } else {
                  textobj.name = '';
                  textobj.word = '';
                  textlog.push(textobj);
                }
              } else if (textline2[2].startsWith('![[')) {
                const faceurl = value.match(/(?<=\!\[\[).+(?=\|face)/g);
                textobj.url = '![[' + faceurl[0] + ']]';
                const word3 = value.match(/(?<=\]\s)(.*)/g);
                if (!empty(word3)) {
                  const nametext = value.match(/(?<=\]\s\*)(.*?)(?=\*\s)/g);
                  if (!empty(nametext)) {
                    textobj.name = nametext[0];
                    const word4 = value.match(/(?<=\*\s).*$/g);
                    if (!empty(word4)) {textobj.word = word4[0].trim();
                    } else {textobj.word = ''}
                    textlog.push(textobj);
                  } else {
                    textobj.name = '';
                    textobj.word = word3[0].trim();
                    textlog.push(textobj);
                  }
                } else {
                  textobj.name = '';
                  textobj.word = '';
                  textlog.push(textobj);
                }
              } else {
                const word3 = value.substring(4);
                textobj.url = t('t.tag31');
                textobj.name = '';
                textobj.word = word3.trim();
                textlog.push(textobj);
              }
            } else if (textline2[2].startsWith('*')) {
              textobj.url = t('t.tag31');
              textobj.name = textline2[2].replace(/\*/g, '');
              const word3 = value.match(/(?<=\*\s)(.*)/g);
              if (!empty(word3)) {textobj.word = word3[0].trim();
              } else {textobj.word = ''}
              textlog.push(textobj);
            } else {
              const word3 = value.substring(4);
              textobj.url = t('t.tag31');
              textobj.name = '';
              textobj.word = word3.trim();
              textlog.push(textobj);
            }
          };
          if (textline2[1] === '-') {
            textobj.symbol = '-';
            textnext();
          } else if (textline2[1] === '+') {
            textobj.symbol = '+';
            textnext();
          } else {
            const word3 = value.substring(2);
            if (index !== 1 && lines[index - 1] !== '> ' && !empty(lines[index - 1])) {
              textobj.symbol = 'c';
              textobj.word = word3.trim();
              textlog.push(textobj);
            } else {
              textobj.symbol = 'p';
              textobj.word = word3.trim();
              textlog.push(textobj);
            }
          }
        };
      }
    });
    if (textlog.length >= 2) {
      let ccount = findValues(textlog, 'c');
      if (ccount[0]) {
        ccount.forEach(value => {
          const cstart = value.start;
          const cnum = value.count;
          const call = cstart + cnum;
          let text0 = textlog[cstart - 1].word;
          for (var i = cstart; i < call; i++) {
            text0 += '\n' + textlog[i].word;
          }
          textlog[cstart - 1].word = text0;
        });
        let newArray = textlog.filter(function(value) {
          return value.symbol !== 'c';
        });
        textlog = newArray.slice();
      }
    }
    if (showchecknum[0] === 0) {setCode()};
    styleword();
    if (showchecknum2[0] === 1) {editframe()};
    codeRefresh();
  }
}

textareaCode.addEventListener('input', function() {
  this.style.height = 'auto';
  this.style.height = (this.scrollHeight) + 'px';
});

const codebutdiv = document.createElement("div");
codebutdiv.classList.add('chat-codebutdiv');
const codechatONbut = document.createElement("span");
codechatONbut.classList.add('chat-chatOnbut');
const codechatONCheck = createCheckbox('codechatON001', t('t.tip27'), t('t.tip27'));
const codechatONlabel = createLabel('codechatON001', t('t.tip27'));
codechatONlabel.classList.add('chat-label2');
codechatONbut.append(codechatONCheck, codechatONlabel);
codechatONCheck.addEventListener('change', function() {
  textareaCode.focus();
});

const codewordbut = document.createElement("span");
codewordbut.innerHTML = penicon;
codewordbut.ariaLabel = t('t.Input');
codewordbut.classList.add('chat-clear-button2');
codewordbut.onclick = ()=> {
  if (codechatONCheck.checked) {
    codechatON = true;
  } else {
    codechatON = false;
  }
  inputcode(textareaCode.value);
  codechatON = false;
}
const codeclearbut = document.createElement("span");
codeclearbut.innerHTML = deleteicon;
codeclearbut.ariaLabel = t('t.tip28');
codeclearbut.classList.add('chat-clear-button3');
codeclearbut.onclick = ()=> {
  surebox.style.display = 'flex';
  sureResult = 3;
}

function resetCode() {
  titletext = t('t.title');
  inputTitle.value = '';
  textlog = [];
  radionum = 0;
  radionum2 = 1;
  for (var i = 0; i <= 8; i++) {checknum[i] = 0}
  if (showchecknum[0] === 0) {setCode()};
}

function setCode() {
  for (var i = 0; i <= 6; i++) {
    const allradios = document.getElementById(`radio${i}`);
    allradios.checked = false;
    if (i === radionum) {allradios.checked = true;}
  }

  for (var i = 0; i <= 8; i++) {
    const allchecks = document.getElementById(`checkbox${i}`);
    allchecks.checked = false;
    if (checknum[i] === 1) {
      allchecks.checked = true;
    }
  }

  for (var i = 0; i <= 2; i++) {
    const allradios2 = document.getElementById(`radio2${i}`);
    allradios2.checked = false;
    if (i === radionum2) {allradios2.checked = true;}
  }
}

codebutdiv.append(codeclearbut, codechatONbut, codewordbut);
codeEditDiv.append(textareaCode, codebutdiv);

function codeRefresh() {
  if (showchecknum2[1] === 1) {
    textareaCode.value = result2;
    textareaCode.style.height = 'auto';
    textareaCode.style.height = (textareaCode.scrollHeight) + 'px';
  };
}

// 显示编辑框
const showcheckdiv2 = document.createElement("div");
showcheckdiv2.classList.add('chat-menubar');
const options5 = [t('t.name15'), t('t.name16')];
options5.forEach(function(option, index) {
  const checkbox = createCheckbox('showcheckbox4' + index, option, option);
  const label = createLabel('showcheckbox4' + index, option);
  label.ariaLabel = t('t.tip7') + option;
  checkbox.ariaLabel = t('t.tip7') + option;
  if (showchecknum2[index] === 1) {
    checkbox.checked = true;
  }
  label.classList.add('chat-label2');
  showcheckdiv2.append(checkbox, label);
});

if (showchecknum2[0] === 1) {editframe()}
if (showchecknum2[1] === 1) {
  codeShow.appendChild(codeEditDiv);
  textareaCode.value = result2;
}

showcheckdiv2.addEventListener('change', function(event) {
  if (event.target.type === 'checkbox') {
    if (event.target.checked) {
      if (event.target.id === 'showcheckbox40') {
        editframe();
        showchecknum2[0] = 1;
        localStorage.setItem('chatShowchecknum2', JSON.stringify(showchecknum2));
      }
      if (event.target.id === 'showcheckbox41') {
        codeShow.appendChild(codeEditDiv);
        textareaCode.value = result2;
        showchecknum2[1] = 1;
        localStorage.setItem('chatShowchecknum2', JSON.stringify(showchecknum2));
      }
    } else {
      if (event.target.id === 'showcheckbox40') {
        editdiv.innerHTML = "";
        facenum = [];
        if (showchecknum[2] === 0) {fy()};
        showchecknum2[0] = 0;
        localStorage.setItem('chatShowchecknum2', JSON.stringify(showchecknum2));
      }
      if (event.target.id === 'showcheckbox41') {
        codeShow.innerHTML = "";
        showchecknum2[1] = 0;
        localStorage.setItem('chatShowchecknum2', JSON.stringify(showchecknum2));
      }
    }
  }
});
const save = document.createElement("span");
save.innerHTML = obsiIcon2('lucide-save', 16);
save.ariaLabel = t('t.tip29');
save.classList.add('chat-edit-button2');
function savelocal() {
  localStorage.setItem('chatShowchecknum', JSON.stringify(showchecknum));
  localStorage.setItem('chatShowchecknum2', JSON.stringify(showchecknum2));
  localStorage.setItem("chatResult2", result2);
  localStorage.setItem('chatFavid', JSON.stringify(favid));
  localStorage.setItem('chatCharanum', JSON.stringify(charanum));
  localStorage.setItem("chatSort", sort);
  localStorage.setItem("chatListnum", listnum);
}
save.onclick = ()=> {
  savelocal();
  savemeta2();
  new obsidian.Notice(t('t.notice9'));
}
const load = document.createElement("span");
load.innerHTML = obsiIcon2('lucide-download', 16);
load.ariaLabel = t('t.tip30');
load.classList.add('chat-edit-button2');
load.onclick = ()=> {
  codechatONCheck.checked = false;
  result2 = filemeta.result2;
  chattemp = filemeta.favid;
  if (chattemp !== "[]" && chattemp !== "") {
    favid = chattemp.slice();
    if (favid.length !== 0) {
      chattemp = favid.filter(function(value) {
        return value < allfiles.length;
      });
      favid = chattemp.slice();
    }
  } else {favid = []}
  chattemp = filemeta.charanum;
  if (chattemp !== "[]" && chattemp !== "") {
    charanum = chattemp.slice();
    if (charanum.length !== 0) {
      chattemp = charanum.filter(function(value) {
        return value.id < allfiles.length;
      });
      charanum = chattemp.slice();
    }
  } else {charanum = []}
  savelocal();
  inputcode(result2);
  if (inputTitle.value === t('t.title')) {inputTitle.value = ''};
  if (showchecknum[3] === 0) {createChat()};
  fy();
  new obsidian.Notice(t('t.notice10'));
}
const clear = document.createElement("span");
clear.innerHTML = deleteicon;
clear.ariaLabel = t('t.tip32');
clear.classList.add('chat-edit-button2');
clear.onclick = ()=> {
  if (localStorage.hasOwnProperty('chatShowchecknum')) {
    localStorage.removeItem('chatShowchecknum');
  }
  if (localStorage.hasOwnProperty('chatShowchecknum2')) {
    localStorage.removeItem('chatShowchecknum2');
  }
  if (localStorage.hasOwnProperty('chatResult2')) {
    localStorage.removeItem('chatResult2');
  }
  if (localStorage.hasOwnProperty('chatFavid')) {
    localStorage.removeItem('chatFavid');
  }
  if (localStorage.hasOwnProperty('chatCharanum')) {
    localStorage.removeItem('chatCharanum');
  }
  if (localStorage.hasOwnProperty('chatSort')) {
    localStorage.removeItem('chatSort');
  }
  if (localStorage.hasOwnProperty('chatListnum')) {
    localStorage.removeItem('chatListnum');
  }
  clearmeta();
  new obsidian.Notice(t('t.notice11'));
}
const note = document.createElement("span");
note.innerHTML = obsiIcon2('lucide-file-plus-corner', 16);
note.ariaLabel = t('t.tip31');
note.classList.add('chat-edit-button2');
note.onclick = ()=> {newnote(newTitle())}
showcheckdiv2.append(save, load, clear, note);

// 替换html标签
function replaText(textOri, tag1, tag2, tag3, tag4) {
  const reg = new RegExp(tag1 + '(.+?)' + tag2, 'g');
  return textOri.replace(reg, (_, inner) => tag3 + inner + tag4);
}

// 查找连续相同值
function findValues(arr, target) {
  let result = [];
  let count = 0;
  let startIndex = -1;
  for (let i = 0; i < arr.length; i++) {
    if (arr[i].symbol === target) {
      if (count === 0) {
          startIndex = i; // 记录连续序列的起始位置
      }
      count++; // 增加计数
    } else {
      if (count > 0) {
          result.push({ start: startIndex, count: count }); // 添加结果
          count = 0; // 重置计数
          startIndex = -1; // 重置起始位置
      }
    }
  }
  // 检查数组末尾是否有连续的值未被记录
  if (count > 0) {
      result.push({ start: startIndex, count: count });
  }
  return result;
}

// 复制用代码生成和预览
function styleword() {
  chatstyle = '> [!chatbox]';
  for (var i = 1; i <= 6; i++) {
    if (radionum === i) {
      chatstyle = chatstyle.replace(']', '');
      chatstyle += '|' + options[i] + ']';
    }
  }

  for (var i = 0; i <= 8; i++) {
    if (checknum[i] === 1) {
      chatstyle = chatstyle.replace(']', '');
      chatstyle += '-' + options2[i] + ']';
    }
  }

  // 判断是否奇数
  function isOdd(number) {
    return number % 2 !== 0;
  }

  function pNumber(num, arr) {
    let pnum2 = 1;
    for (var i=num; i < arr.length - 1; i++) {
      if (arr[i].symbol === 'p' && arr[i].symbol === arr[i + 1].symbol) {pnum2++} else {break;}
    }
    return pnum2
  }

  if (textlog[0]) {
    if (textlog[0].symbol === '+') {
      chatstyle = chatstyle.replace(']', '');
      chatstyle += '-swap]';
    }
    if (textlog[0].symbol === 'p') {
      let pnum = 0;
      for (var i=0; i < textlog.length; i++) {
        if (textlog[i].symbol === 'p') {pnum++}
      }
      if (pnum !== textlog.length) {
        pnum = pNumber(0, textlog);
        if (isOdd(pnum)) {
          if (textlog[pnum].symbol === '-') {
            chatstyle = chatstyle.replace(']', '');
            chatstyle += '-swap]';
          }
        } else {
          if (textlog[pnum].symbol === '+') {
            chatstyle = chatstyle.replace(']', '');
            chatstyle += '-swap]';
          }
        }
      }
    }
  }

  chatstyle = chatstyle.replace('box-', 'box|');

  if (titletext !== '' && checknum[0] === 0) {
    if (radionum2 === 0) {
      chatstyle += ' ';
    } else if (radionum2 === 1) {
      chatstyle += '+ ';
    } else {
      chatstyle += '- ';
    }
  }

  if (textlog[0]) {
    textshow = textlog.slice();
    if (textlog.length >= 3) {
      let pcount = findValues(textshow, 'p');
      if (pcount[0]) {
        let editem = 0;
        pcount.forEach(function(value, index) {
          const pstart = value.start + editem;
          const pnum3 = value.count;
          const pall = pstart + pnum3;
          let emobj = {};
          if (pstart !== 0 && pall !== textshow.length) {
            if (textshow[pstart - 1].symbol === '-') {
              if (isOdd(pnum3)) {
                if (textshow[pall].symbol === '+') {
                  emobj.symbol = 'p';
                  emobj.word = '<span></span>';
                  editem++;
                  textshow.splice(pall,0,emobj);
                }
              } else {
                if (textshow[pall].symbol === '-') {
                  emobj.symbol = 'p';
                  emobj.word = '<span></span>';
                  editem++;
                  textshow.splice(pall,0,emobj);
                }
              }
            } else {
              if (isOdd(pnum3)) {
                if (textshow[pall].symbol === '-') {
                  emobj.symbol = 'p';
                  emobj.word = '<span></span>';
                  editem++;
                  textshow.splice(pall,0,emobj);
                }
              } else {
                if (textshow[pall].symbol === '+') {
                  emobj.symbol = 'p';
                  emobj.word = '<span></span>';
                  editem++;
                  textshow.splice(pall,0,emobj);
                }
              }
            }
          }
        });
      }
    }
  }

  newtext = '';
  if (!textlog[0]) {newtext = yulan;
  } else {
    textshow.forEach(function(value, index) {
      if (value.symbol !== 'p') {
        newtext += '\n\> ' + value.symbol;
        newtext += ifLocalPicWord(value.url);
        if (value.name !== '') {newtext += ' *' + value.name +'*'};
      } else {
        newtext += '\n\> \n\>';
      }
      const wordtext = value.word.split("\n");
      let wordflat = [];
      for (var i=0; i < wordtext.length; i++) {
        if (!empty(wordtext[i])) {wordflat.push(wordtext[i].trim())}
      }
      for (var i=0; i < wordflat.length; i++) {
        let tempwordflat = wordflat[i];
        if (checknum[8] === 1) {
          tempwordflat = replaText(tempwordflat, '\\*\\*', '\\*\\*', '<b>', '</b>');
          tempwordflat = replaText(tempwordflat, '\\*', '\\*', '<em>', '</em>');
          tempwordflat = replaText(tempwordflat, '==', '==', '<mark>', '</mark>');
          tempwordflat = replaText(tempwordflat, '~~', '~~', '<del>', '</del>');
        } else {
          tempwordflat = replaText(tempwordflat, '<b>', '<\\/b>', '**', '**');
          tempwordflat = replaText(tempwordflat, '<em>', '<\\/em>', '*', '*');
          tempwordflat = replaText(tempwordflat, '<mark>', '<\\/mark>', '==', '==');
          tempwordflat = replaText(tempwordflat, '<del>', '<\\/del>', '~~', '~~');
        }
        if (i === 0) {
          newtext += ' ' + tempwordflat;
        } else {
          newtext += '\n\> ' + tempwordflat;
        }
      }
    });
  }

  removeSpan();
  if (checknum[0] === 1) {
    if (!textlog[0]) {
      result1 = '```markdown\n' + chatstyle + '\n```';
      result2 = chatstyle;
    } else {
      result1 = '```markdown\n' + chatstyle + newtext + '\n```';
      result2 = chatstyle + newtext;
    }
    yulantext = chatstyle + newtext;
  } else {
    if (!textlog[0]) {
      result1 = '```markdown\n' + chatstyle + titletext + '\n```';
      result2 = chatstyle + titletext;
    } else {
      result1 = '```markdown\n' + chatstyle + titletext + newtext + '\n```';
      result2 = chatstyle + titletext + newtext;
    }
    yulantext = chatstyle + titletext + newtext;
  }
  localStorage.setItem("chatResult2", result2);
  dv.span(yulantext);
  dv.span(result1);
}

// 生成笔记
function formatDateTime(date) {
  function padZero(num) {
    return num < 10 ? '0' + num : num;
  }
  const year = date.getFullYear();
  const month = padZero(date.getMonth() + 1);
  const day = padZero(date.getDate());
  const hours = padZero(date.getHours());
  const minutes = padZero(date.getMinutes());
  creatTime = year + '-' + month + '-' + day + ' ' + hours + ':' + minutes;
  return year + month + day + hours + minutes;
}
function newTitle() {
  const currentDateTime = new Date();
  const formattedDateTime = formatDateTime(currentDateTime);
  if (checknum[0] === 1) {
    mdtitle = formattedDateTime;
    mdalias = mdtitle;
  } else {
    if (empty(titletext)) {
      mdtitle = formattedDateTime;
      mdalias = mdtitle;
    } else {
      let titletemp = titletext.replace(/[<>\*\|\\\/:"'&#%\[\]\{\}]/g, '');
      titletemp = titletemp.replace(/\?/g, '？')
      mdtitle = formattedDateTime + '_' + titletemp;
      mdalias = formattedDateTime + ' ' + titletemp;
    }
  }
  const textTitle = `${notefolder}${mdtitle}.md`
  return textTitle;
}

function lastFileName() {
  let lastFile = '';
  let notefolder2 = notefolder;
  if (empty(notefolder2)) {
    notefolder2 = '';
  } else {
    notefolder2 = notefolder2.substring(0, notefolder2.length - 1);
    notefolder2 = `"${notefolder2}"`;
  }
  const notefile = dv.pages(notefolder2)
    .sort(p => p.file.ctime, 'desc')
    .limit(1);
  if (notefile.length !== 0) {
    if (showchecknum[4] !== 0) {
      lastFile = notefile.file.path[0] + '|' + notefile.file.name[0];
    } else {
      lastFile = notefile.file.name[0];
    }
  } else {lastFile = ''}
  return lastFile;
}

async function newnote(route) {
  let creatOK = 0;
  if (!empty(notefolder)) {
    const folderExists = await app.vault.adapter.exists(notefolder);
    if (!folderExists) {new obsidian.Notice(t('t.notice12'));
    } else {creatOK = 1}
  } else {creatOK = 1}
  if (creatOK === 1) {
    const fileExists = await app.vault.adapter.exists(route);
    if (fileExists) {
      new obsidian.Notice(t('t.notice13'));
    } else {
      if (empty(templatePath)) {
        await app.vault.create(route, result2);
      } else {
        const fileExists3 = await app.vault.adapter.exists(templatePath);
        if (!fileExists3) {
          new obsidian.Notice(t('t.notice14'));
          await app.vault.create(route, result2);
        } else {
          const templateFile = await app.vault.getAbstractFileByPath(templatePath);
          let tempContent = await app.vault.cachedRead(templateFile);
          if (tempContent.includes('{title}')) {
            tempContent = tempContent.replace(/{title}/g, mdtitle);}
          if (tempContent.includes('{alias}')) {
            tempContent = tempContent.replace(/{alias}/g, mdalias);}
          if (tempContent.includes('{time}')) {
            tempContent = tempContent.replace(/{time}/g, creatTime);}
          if (tempContent.includes('{file}')) {
            tempContent = tempContent.replace(/{file}/g, lastFileName());}
          if (tempContent.includes('{result}')) {
            tempContent = tempContent.replace(/{result}/g, result2);
          } else {tempContent += '\n' + result2}
          await app.vault.create(route, tempContent);
        }
      }
      new obsidian.Notice(t('t.notice15'));
    }
  }
}

// 合并
const allContainer = document.createElement("div");
allContainer.addEventListener('click', function(e) {
  if (e.target.tagName === 'IMG') {e.preventDefault()}
});
allContainer.append(showcheckdiv, styleselediv, folderselediv, charaselediv, charachatdiv, showcheckdiv2, codeShow, editdiv, surebox);
dv.span(allContainer);
dv.span(yulantext);
dv.span(result1);
inputcode(result2);
if (inputTitle.value === t('t.title')) {inputTitle.value = ''};
fy();
```


# 最新5篇对话笔记 Latest 5 Chat Notes

```dataviewjs
let notefolder = dv.current().file.frontmatter.notefolder;
if (!notefolder) {
  notefolder = '';
} else {
  notefolder = notefolder.substring(0, notefolder.length - 1);
  notefolder = `"${notefolder}"`;
}
let text = '> [!chatbox|notitle-noname-noface] ';
const notefiles = dv.pages(notefolder)
  .sort(p => p.file.ctime, 'desc')
  .limit(5);
notefiles.map((p, index) => {
  if (index % 2 === 0) {
    text += '\n\> + **' + p.file.link + '**';
  } else {
    text += '\n\> - **' + p.file.link + '**';
  }
});
dv.span(text)
```


# 清除本地数据 Clear local data

```dataviewjs
const lang = window.moment.locale() && window.moment.locale().startsWith('zh') ? 'zh' : 'en';
//翻译文本
const I18N = {
  zh: {
    't.label':'清除本地数据', 't.hint':'如果本地存储数据导致读取错误，请先清除！', 't.notice':'已清除本地数据！',
  },
  en: {
    't.label':'Clear Local Data', 't.hint':'If reading errors occur due to locally stored data, please clear it first!', 't.notice':'Local data has been cleared!',
  }
};

function t(key) {
  let s = (I18N[lang] || I18N.zh)[key];
  if (s === undefined) s = key;
  return s;
}

function obsiIcon2(iconid, size) {
  const icon = document.createElement('span');
  obsidian.setIcon(icon, iconid);
  icon.classList.add('chat-icon-resize');
  icon.style.setProperty('--icon-svg-width', `${size}px`);
  icon.classList.add('chat-icon-center');
  return icon.outerHTML;
}
const clear = document.createElement("span");
clear.innerHTML = obsiIcon2('lucide-eraser', 16);
clear.ariaLabel = t('t.label');
clear.classList.add('chat-clear-button3');
clear.onclick = ()=> {
  if (localStorage.hasOwnProperty('chatShowchecknum')) {
    localStorage.removeItem('chatShowchecknum');
  }
  if (localStorage.hasOwnProperty('chatShowchecknum2')) {
    localStorage.removeItem('chatShowchecknum2');
  }
  if (localStorage.hasOwnProperty('chatResult2')) {
    localStorage.removeItem('chatResult2');
  }
  if (localStorage.hasOwnProperty('chatFavid')) {
    localStorage.removeItem('chatFavid');
  }
  if (localStorage.hasOwnProperty('chatCharanum')) {
    localStorage.removeItem('chatCharanum');
  }
  if (localStorage.hasOwnProperty('chatSort')) {
    localStorage.removeItem('chatSort');
  }
  if (localStorage.hasOwnProperty('chatListnum')) {
    localStorage.removeItem('chatListnum');
  }
  new obsidian.Notice(t('t.notice'));
}
const text = document.createElement("span");
text.textContent = t('t.hint');
text.style.marginLeft = '1rem';
const alldiv = document.createElement("div");
alldiv.classList.add('chat-inputbox');
alldiv.appendChild(clear);
alldiv.appendChild(text);
dv.span(alldiv);

let clearText = `> [!chatbox|noname-noface]- 清除数据详情
> - 清除存储在localStorage中的以下键值
> chatShowchecknum：样式/文件夹等的显示设定
> chatShowchecknum2：编辑框和代码框的显示
> chatResult2：代码结果
> chatFavid：置顶卡片id
> chatCharanum：角色对话框id
> chatSort：排序方式
> chatListnum：每页显示数量
> - 对本文档**YAML**的存储数据无影响`;
if (lang !== 'zh') {
  clearText = `> [!chatbox|noname-noface]- Clear data details
> - Clear the following key-value pairs stored in localStorage.
> chatShowchecknum: Display settings for styles/folders, etc
> chatShowchecknum2: Display of edit boxes and code boxes
> chatResult2: Code result
> chatFavid: Pin card id
> chatCharanum: Character dialog box ID
> chatSort: Sorting method
> chatListnum: Number of items displayed per page
> - It has no impact on the stored data in  **YAML**  format in this document.`;
}

dv.span(clearText);
```