---
layout: widget 
title: Widget
hide: true
permalink: /chapter/widget/widget/
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/7.4.4/d3.min.js"></script>
<div id="treemap-detel"></div>

<script type="module">
import { setupSvg, setupTreemap } from "/detel-book/assets/js/treemap_module.js";

const helpText = `
Welcome to the Learning Goals Widget <br/> <br/>
This tool helps you reflect on the topics you learned
and keeps track of your progress.
On the left side there are the topics and on right side
the learning goals. Each of these goals has a percent near
it representing your progress so far. <br/>
You can change this value, by clicking on the topic or on
the learning goal and then moving the slider
to the desired position. On the right side of each topic
there is an average of the progress that you made on the
learning goals. <br/> <br/>
If you are using a screen reader, you can navigate through the document
with the Tab key. By pressing enter you can expand the topics.
When an action for the keyboard is available, it will be announced.
This tool is optimized for Google Chrome and its extension called
Screen Reader. For an optimal experience we suggest you to use those. <br/>
Under the accessibility icon you can find two buttons to change
the size of the font. If instead you would like to change the zoom
you can press Ctrl and + or Ctrl and -. <br/>
The third icon is used to change the colors of the widget. <br/>
If you are colorblind, there you can find some colorschemes,
that have a dark blue outline. These have a high contrast and
should be suitable to you. <br/> <br/>
We wish you a happy learning experience!`;

const taxonomyCont = JSON.parse(`
{
	"name": "IDSAI",
	"children": [{
		"name": "Overview - Data Science and Artificial intelligence",
		"type": "topic",
		"keyword": "Overview Data Science and AI",
		"link": "https:\\\/\\\/tc.tugraz.at\\\/main\\\/pluginfile.php\\\/181506\\\/mod_resource\\\/content\\\/1\\\/1a%20-%20IDSAI%202020%20Intro",
		"children": [{
			"name": "Understand what data science is",
			"keyword": "Data Science",
			"link": "https://www.know-center.tugraz.at/en/"
		}, {
			"name": "Understand what artificial intelligence is",
			"keyword": "Artificial Intelligence",
			"link": ""
		}, {
			"name": "Remember, understand and apply different definitions of intelligence",
			"keyword": "Definitions of intelligence",
			"link": ""
		}, {
			"name": "Remember and explain building blocks of intelligent systems",
			"keyword": "Building blocks of intelligent systems",
			"link": ""
		}, {
			"name": "Remember, understand and give examples for knowledge representation formalisms + reasoning mechanism",
			"keyword": "Knowledge representation and reasoning",
			"link": ""
		}]
	}, {
		"name": "Rules",
		"type": "topic",
		"keyword": "Rules",
		"link": "",
		"children": [{
			"name": "Understand the basic components of a rule",
			"keyword": "Rule components",
			"link": ""
		}, {
			"name": "Understand the main components of a rule-based system",
			"keyword": "Rule-based system components",
			"link": ""
		}, {
			"name": "Apply forward chaining",
			"keyword": "Forward chaining",
			"link": ""
		}, {
			"name": "Apply backward chaining",
			"keyword": "Backward chaining",
			"link": ""
		}]
	}, {
		"name": "Logic",
		"type": "topic",
		"keyword": "",
		"link": "",
		"children": [{
			"name": "Understand what are facts and what is general knowledge in knowledge representation",
			"keyword": "Facts and general knowledge",
			"link": ""
		}, {
			"name": "Understand logic as object-oriented knowledge representation",
			"keyword": "Logic as object-oriented KR",
			"link": ""
		}, {
			"name": "Understand core modelling constructs",
			"keyword": "",
			"link": ""
		}, {
			"name": "Be able to reason over core modelling constructs",
			"keyword": "Reason over core modelling constructs",
			"link": ""
		}]
	}, {
		"name": "Graphs",
		"type": "topic",
		"keyword": "",
		"link": "",
		"children": [{
			"name": "Define different types of graphs",
			"keyword": "Types of Graphs",
			"link": ""
		}, {
			"name": "Understand semantic networks",
			"keyword": "Semantic Networks",
			"link": ""
		}, {
			"name": "Explain and use spreading activation",
			"keyword": "Spreading activation",
			"link": ""
		}, {
			"name": "Explain common graph measures",
			"keyword": "Common graph measures",
			"link": ""
		}, {
			"name": "Understand and use common graph measures for reasoning",
			"keyword": "Common graph measures for reasoning",
			"link": ""
		}]
	}, {
		"name": "Vectors as Knowledge Representation",
		"type": "topic",
		"keyword": "Vectors as KR",
		"link": "",
		"children": [{
			"name": "Understand, explain, and give example vector representations of complex items.",
			"keyword": "Vectors as representations of complex items",
			"link": ""
		}, {
			"name": "Give example symbolic descriptions of complex items",
			"keyword": "Symbolic descriptions of complex entities",
			"link": ""
		}, {
			"name": "Understand and explain vector operations as way to reason over vectors",
			"keyword": "Cosine similarity",
			"link": ""
		}, {
			"name": "Understand the relevance of similarity measures in computational problems",
			"keyword": "Relevance of similarity measures",
			"link": ""
		}]
	}, {
		"name": "Information Retrieval",
		"type": "topic",
		"keyword": "IR",
		"link": "",
		"children": [{
			"name": "Define information retrieval",
			"keyword": "Define IR",
			"link": ""
		}, {
			"name": "Understand TFIDF and the rationale for it",
			"keyword": "Understand TFIDF",
			"link": ""
		}, {
			"name": "List and describe challenges in natural language processing relevant for IR",
			"keyword": "List and describe NLP challenges relevant for IR",
			"link": ""
		}, {
			"name": "Compute term frequency and TFIDF vectors for documents and queries",
			"keyword": "Compute TF and TFIDF vectors for documents and queries",
			"link": ""
		}]
	}, {
		"name": "Recommender Systems",
		"type": "topic",
		"keyword": "Recommenders",
		"link": "",
		"children": [{
			"name": "Define the computational task of recommenation",
			"keyword": "Define recommendation",
			"link": ""
		}, {
			"name": "Explain what a user model is",
			"keyword": "Explan user model",
			"link": ""
		}, {
			"name": "Carry out user-based collaborative filtering",
			"keyword": "Carry out user-based collaborative filtering",
			"link": ""
		}, {
			"name": "Carry out item-based collaborative filtering",
			"keyword": "Carry out item-based collaborative filtering",
			"link": ""
		}, {
			"name": "Compare user-based and item-based collaborative filtering",
			"keyword": "Compare user- and item-based CF",
			"link": ""
		}, {
			"name": "Compare Recommendation and Information Retrieval",
			"keyword": "Compare recommendation with IR",
			"link": ""
		}]
	}, {
		"name": "Artificial Neural Networks",
		"type": "topic",
		"keyword": "ANNs",
		"link": "",
		"children": [{
			"name": "Understand what machine learning is",
			"keyword": "Understand what ML is",
			"link": ""
		}, {
			"name": "Understand the machine learning task classification ",
			"keyword": "Understand classification (what it is)",
			"link": ""
		}, {
			"name": "Understand the principles of the human brain, and the analogy to neural networks",
			"keyword": "Understand the human brain (basics)",
			"link": ""
		}, {
			"name": "Describe the McCulloch-Pitts Neuron",
			"keyword": "Describe the McCulloch-Pitts Neuron",
			"link": ""
		}, {
			"name": "Express a boolean formula as a McCulloch Pitts Net, and vice versa",
			"keyword": "Express a boolean formula as an ANN",
			"link": ""
		}, {
			"name": "Express single-layer Perceptron Network as linear equation, and vice versa",
			"keyword": "Express single-layer Perceptron Network as linear equation, and vice versa",
			"link": ""
		}]
	}, {
		"name": "Machine Learning (Perceptron Learning)",
		"type": "topic",
		"keyword": "ML",
		"link": "https://www.know-center.tugraz.at/en/",
		"children": [{
			"name": "Understand classification in comparison to (linear) equation solving",
			"keyword": "Understand classification",
			"link": ""
		}, {
			"name": "Describe the perceptron learning algorithm",
			"keyword": "Describe the perceptron learning algorithm",
			"link": "https://www.know-center.tugraz.at/en/"
		}, {
			"name": "Carry out the perceptron learning algorithm",
			"keyword": "Carry out the perceptron learning algorithm",
			"link": ""
		}]
	}]
}
`);
/**
 * Returns a hash code from a string
 * @param  {String} str The string to hash.
 * @return {Number}    A 32bit integer
 * @see http://werxltd.com/wp/2010/05/13/javascript-implementation-of-javas-string-hashcode-method/
 */
function hashCode(str) {
    let hash = 0;
    for (let i = 0, len = str.length; i < len; i++) {
        let chr = str.charCodeAt(i);
        hash = (hash << 5) - hash + chr;
        hash |= 0; // Convert to 32bit integer
    }
    return hash;
}

const treemapID = "treemap-detel";
const localStorageKey = "treemapProgress";

const generateLocalStorageEntry = () => {
  const obj = {};
  obj[treemapID] = {};
  taxonomyCont.children.forEach((topic) => {
    topic.children.forEach((learningGoal) => {
      const name = topic.name + "@" + learningGoal.name;
      const hash = hashCode(name);
      obj[treemapID][hash] = 0;
    });
  });
  localStorage.setItem(localStorageKey, JSON.stringify(obj));
  return obj;
};

const getProgress = () => {
  let progress = localStorage.getItem(localStorageKey);
  if (progress === null) {
    progress = generateLocalStorageEntry();
  } else {
    progress = JSON.parse(progress);
  }

  taxonomyCont.children.forEach((topic) => {
    topic.children.forEach((learningGoal) => {
      const name = topic.name + "@" + learningGoal.name;
      const hash = hashCode(name);
      learningGoal.pro = progress[treemapID][hash];
    });
  });
};

const saveProgress = (_, object, pro) => {
  const name = object.parent.data.name + "@" + object.data.name;
  const hash = hashCode(name);
  let progress = localStorage.getItem(localStorageKey);
  if (progress === null) {
    progress = generateLocalStorageEntry();
  } else {
    progress = JSON.parse(progress);
  }
  progress[treemapID][hash] = parseFloat(pro);
  localStorage.setItem(localStorageKey, JSON.stringify(progress));
};

const retrieveProgress = () => {
  let progress = localStorage.getItem(localStorageKey);
  if (progress === null) {
    progress = generateLocalStorageEntry();
  } else {
    progress = JSON.parse(progress);
  }

  taxonomyCont.children.forEach((topic) => {
    topic.children.forEach((learningGoal) => {
      const name = topic.name + "@" + learningGoal.name;
      const hash = hashCode(name);
      learningGoal.pro = progress[treemapID][hash];
    });
  });
};

retrieveProgress();
setupTreemap(taxonomyCont, d3, treemapID, helpText, true, saveProgress);
setupSvg();

</script>

